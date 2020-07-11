---
title: Evaluation procedures
permalink: /docs/evaluation/
---

# WORK IN PROGRESS! 


In the following, we give a short overview on how to use the datasets together with the graph kernel and GNN baselines and standardized evaluation methods. 
First follow the instruction on [github.com/chrsmrrs/tudataset](https://github.com/chrsmrrs/tudataset) to install the TUDataset Python package. 

Throught this tutorial, we assume that your base directiory is `tudataset/tud_benchmark/`.

### Kernel baselines and 10-CV using SVMs

We provide  Python-wrapped C++ implementations of the following kernels:
- Weisfeiler-Lehman subtree kernel (1-WL) [1],
- Graphlet kernel (GR) [2],
- Shortest-path kernels (SP) [3],
- Weisfeiler-Lehman optimal assignment kernel (WL-OA) [4]


For the  first three kernels, we provide, both, Gram matrix output (`numpy.array`, `[n,n]`) and sparse feature vector output (`scipy.sparse.csr_matrix`, `[n,d]`).

#### Weisfeiler-Lehman subtree kernel

The following code will download the `ENZYMES` dataset, compute the 1-WL for `3` iterations using the discrete node labels of the dataset, and output the Gram matrix as a `numpy.array`.

```python
import kernel_baselines as kb
import auxiliarymethods.datasets as dp

use_labels, use_edge_labels = True, False
dataset = "ENZYMES"

dp.get_dataset(dataset)

iterations = 3
gram_matrix = kb.compute_wl_1_dense(dataset, iterations, use_labels, use_edge_labels)
```

Instead of computing the Gram matrix, we can skip Gram matrix computation and output a `scipy.sparse.csr_matrix` feature vector for each graph by replacing the last line by
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

#### Shortest-path kernels

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

The following

### GNNs baselines and 10-CV evaluation

TODO



### Bibliograpphy

[1] 

[2]

[3]

[4]