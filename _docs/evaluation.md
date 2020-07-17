---
title: Tutorial on baseline and evaluation procedures
permalink: /docs/evaluation/
---

In the following, we give a short overview on how to use the dataset collection together with the graph kernel and GNN baselines and standardized evaluation methods. 
First, follow the instruction on [github.com/chrsmrrs/tudataset](https://github.com/chrsmrrs/tudataset) to install the TUDataset Python package. 

Throughout this tutorial, we assume that your base directory is `tudataset/tud_benchmark/`.

### Kernel baselines and 10-CV using SVMs

We provide  Python-wrapped C++ implementations of the following kernels:
- Weisfeiler-Lehman subtree kernel (1-WL) [1],
- Graphlet kernel (GR) [2],
- Shortest-path kernel (SP) [3],
- Weisfeiler-Lehman optimal assignment kernel (WL-OA) [4]


For the  first three kernels, we provide, both, Gram matrix output (`numpy.array`, `[n,n]`) and sparse feature vector output (`scipy.sparse.csr_matrix`, `[n,d]`).

#### Weisfeiler-Lehman subtree kernel

The following code will download the `ENZYMES` dataset, compute the 1-WL for `3` iterations using the discrete node labels of the dataset, and output the Gram matrix as a `numpy.array`. 
Since the dataset does not provide edge labels we set `se_edge_labels = False`.
```python
import kernel_baselines as kb
import auxiliarymethods.datasets as dp

use_labels, use_edge_labels = True, False
dataset = "ENZYMES"

# Download dataset.
classes = dp.get_dataset(dataset)

iterations = 3
gram_matrix = kb.compute_wl_1_dense(dataset, iterations, use_labels, use_edge_labels)
```

Instead of computing the Gram matrix, we can skip its computation and output a `scipy.sparse.csr_matrix` feature vector for each graph by replacing the last line by
```python
feature_vectors = kb.compute_wl_1_sparse(dataset, iterations, use_labels, use_edge_labels)
```

#### Graphlet kernel

Similarly, the Gram matrix for the Graphlet kernel can be computed by
```python
gram_matrix = kb.compute_graphlet_dense(dataset, use_labels, use_edge_labels)
```

The sparse feature vectors can be computed by
```python
feature_vectors = kb.compute_graphlet_sparse(dataset, use_labels, use_edge_labels)
```

#### Shortest-path kernel

The Gram matrix for the Shortest-path kernel can be computed by
```python
gram_matrix = kb.compute_graphlet_dense(dataset, use_labels, use_edge_labels)
```

The sparse feature vectors can be computed by
```python
feature_vectors = kb.compute_graphlet_sparse(dataset, use_labels, use_edge_labels)
```

#### Weisfeiler-Lehman optimal assignment kernel

The Gram matrix for the WL-OA kernel can be computed by
```python
gram_matrix = kb.compute_wloa_dense(dataset, use_labels, use_edge_labels)
```

#### SVM evaluation

Here, we show how to jointly optimize the number of iterations of the 1-WL and the `C` parameter of the (dual) SVM using 10-CV. See the paper on details on the evaluation procedure.

The following code computes the 1-WL for `1` to `5` iterations, and applies cosine normalization. The number of iterations is then jointly optimized with the `C` parameter (`C=[10**3, 10**2, 10** 1, 10**0, 10**-1, 10**-2, 10**-3]`) using 10-CV.
The experiment is repeated `10` times and the average accuracy, the standard deviations over all `10` 10-CV runs and all `100` runs are output.

```python
all_matrices = []
num_reps = 10

# 1-WL kernel, number of iterations in [1:6].
for i in range(1, 6):
    gm = kb.compute_wl_1_dense(dataset, i, use_labels, use_edge_labels)
    # Cosine normalization.
    gm = aux.normalize_gram_matrix(gm)
    all_matrices.append(gm)

accuracy, std_10, std_100 = kernel_svm_evaluation(all_matrices, classes, num_repetitions=num_reps, all_std=True)
```
Similarly, we can do the same for sparse feature vectors using a linear SVM.
```python
feature_vectors = []

# 1-WL feature vectors, number of iterations in [1:6].
for i in range(1, 6):
    fv = kb.compute_wl_1_sparse(dataset, i, use_labels, use_edge_labels)
    # \ell_2 normalization.
    fv = aux.normalize_feature_vector(fv)
    feature_vectors.append(fv)

accuracy, std_10, std_100 = linear_svm_evaluation(feature_vectors, classes, num_repetitions=num_reps, all_std=True)
```

See `main_kernel.py` for more examples.

### GNNs baselines and 10-CV evaluation

Here, we show how to optimize the hyperparameters (number of layers  in `{1,2,3,4,5}`, hidden dimension `{32,64,128}`) of the `GIN` layer [5] using 10-CV.
We set the maximum number of epochs to `200`, the batch size to `64`, the starting learing rate to `0.01`, and the number of repetitions of the 10-CV to `10`.

```python
import auxiliarymethods.datasets as dp
from auxiliarymethods.gnn_evaluation import gnn_evaluation
from gnn_baselines.gnn_architectures import GIN

dataset = "ENZYMES"
dp.get_dataset(dataset)

accuracy, std_10, std_100 = gnn_evaluation(GIN, dataset, [1, 2, 3, 4, 5], [32, 64, 128], max_num_epochs=200, batch_size=64, start_lr=0.01, num_repetitions=num_reps, all_std=True)
```
In case the dataset includes edge labels or (continuous) attributes you can use the `GINE` layer.
```python
import auxiliarymethods.datasets as dp
from auxiliarymethods.gnn_evaluation import gnn_evaluation
from gnn_baselines.gnn_architectures import GINE

dataset = "Yeast"

dp.get_dataset(dataset)

accuracy, std_10, std_100 = gnn_evaluation(GINE, dataset, [1, 2, 3, 4, 5], [32, 64, 128], max_num_epochs=200, batch_size=64, start_lr=0.01, num_repetitions=num_reps, all_std=True)
```
See `main_gnn.py` for more examples. More compatible GNN layers are available from [Pytorch Geometric](https://github.com/rusty1s/pytorch_geometric/tree/master/benchmark/kernel).


### Loading the graphs as NetworkX graphs

TODO


### Bibliograpphy

[1] [1-WL kernel paper](http://www.jmlr.org/papers/volume12/shervashidze11a/shervashidze11a.pdf)

[2] [Graphlet kernel paper](http://proceedings.mlr.press/v5/shervashidze09a/shervashidze09a.pdf)

[3] [Shortest-path kernel paper](https://ieeexplore.ieee.org/document/1565664)

[4] [WL-OA kernel paper](https://papers.nips.cc/paper/6166-on-valid-optimal-assignment-kernels-and-applications-to-graph-classification.pdf)

[5] [GIN paper](https://openreview.net/forum?id=ryGs6iA5Km)