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
Since the dataset does not provide edge labels we set `se_edge_labels = False`
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
The following code computes the 1-WL for `1` to `6` iterations, and applies cosine normalization. The number of iterations is then jointly optimized with the `C` parameter (`C=[10**3, 10**2, 10** 1, 10**0, 10**-1, 10**-2, 10**-3]`) using 10-CV.
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

### GNNs baselines and 10-CV evaluation

Here, we show how to optimize the hyperparameters (number of layers  in `{1,2,3,4,5}`, hidden dimension `{32,64,128}`) of the GIN layer [5] using 10-CV.

```python
import auxiliarymethods.datasets as dp
from auxiliarymethods.gnn_evaluation import gnn_evaluation
from gnn_baselines.gnn_architectures import GIN

use_labels, use_edge_labels = True, False
dataset = "ENZYMES"

dp.get_dataset(dataset)

accuracy, std_10, std_100 = gnn_evaluation(GIN, dataset, [1, 2, 3, 4, 5], [32, 64, 128], max_num_epochs=200, batch_size=64, start_lr=0.01, num_repetitions=num_reps, all_std=True)
```

TODO: Add exampple for datasets with edge labels. 
TODO: Add more details!


### Loading the graphs as NetworkX graphs

TODO


### Bibliograpphy

[1] http://www.jmlr.org/papers/volume12/shervashidze11a/shervashidze11a.pdf

[2] http://proceedings.mlr.press/v5/shervashidze09a/shervashidze09a.pdf

[3] https://ieeexplore.ieee.org/document/1565664

[4] https://papers.nips.cc/paper/6166-on-valid-optimal-assignment-kernels-and-applications-to-graph-classification.pdf

[5] https://openreview.net/forum?id=ryGs6iA5Km