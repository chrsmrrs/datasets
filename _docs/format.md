---
title: File Format
permalink: /docs/format/
---



The data sets have the following format (replace `DS` by the name of the data set):

Let

* `n` = total number of nodes
* `m` = total number of edges
* `N` = number of graphs

1. `DS_A.txt` (`m` lines): sparse (block diagonal) adjacency matrix for all graphs, each line corresponds to `(row, col)` resp. `(node_id, node_id)`. All graphs are undirected. Hence, `DS_A.txt` contains two entries for each edge.
2. `DS_graph_indicator.txt` (`n` lines): column vector of graph identifiers for all nodes of all graphs, the value in the i-th line is the `graph_id` of the node with `node_id i`
3. `DS_graph_labels.txt` (`N` lines): class labels for all graphs in the data set, the value in the i-th line is the class label of the graph with `graph_id i`

There are optional files if the respective information is available:

* `DS_node_labels.txt` (`n` lines): column vector of node labels, the value in the i-th line corresponds to the node with `node_id i`
* `DS_edge_labels.txt` (`m` lines; same size as `DS_A_sparse.txt`): labels for the edges in `DS_A_sparse.txt`
* `DS_node_attributes.txt` (`n` lines): matrix of node attributes, the comma seperated values in the i-th line is the attribute vector of the node with `node_id i`
* `DS_edge_attributes.txt` (`m` lines; same size as `DS_A.txt`): attributes for the edges in `DS_A.txt`
* `DS_graph_attributes.txt` (`N` lines): regression values for all graphs in the data set, the value in the i-th line is the attribute of the graph with `graph_id i`

The datasets can also we easily accessed from popular graph deep libraries, see [here](https://chrsmrrs.github.io/datasets/docs/deep/).