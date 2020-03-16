---
title: Welcome
permalink: /docs/home/
redirect_from: /docs/index.html
---
### News

* 02.03.2020: Added three new data sets from [29].
* 14.01.2020: Added twenty-four new data sets from [24].
* 28.08.2019: Added twenty-two new data sets from [28].
* 09.07.2019: Added two new data sets from [27].
* 23.10.2018: Added five new data sets from [26].
* 13.02.2018: Added Cuneiform data set from [25].
* 11.05.2017: Added twelve new data sets from [24].
* 17.06.2016: Added Synthie data set from [21].
* 10.05.2016: Added eight new data sets from [16].
* 19.04.2016: Added FRANKENSTEIN data set from [15].
* 13.04.2016: Added SYNTHETICnew data set from [3,10].
* 08.04.2016: Added six new data sets from [14].



---
title: Datasets
permalink: /docs/home/
redirect_from: /docs/index.html
---
### Datasets

| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |


R(N) are regression datasets with N tasks per graph.

### File Format

The data sets have the following format (replace `DS` by the name of the data set):

Let

* `n` = total number of nodes
* `m` = total number of edges
* `N` = number of graphs

1. `DS_A.txt` (`m` lines): sparse (block diagonal) adjacency matrix for all graphs, each line corresponds to `(row, col)` resp. `(node_id, node_id)`. All graphs are undirected. Hence, `DS_A.txt` contains two entries for each edge.
2. `DS_graph_indicator.txt` (`n` lines): column vector of graph identifiers for all nodes of all graphs, the value in the i-th line is the `graph_id` of the node with `node_id i`
3. `DS_graph_labels.txt` (`N` lines): class labels for all graphs in the data set, the value in the i-th line is the class label of the graph with `graph_id i`
4. `DS_node_labels.txt` (`n` lines): column vector of node labels, the value in the i-th line corresponds to the node with `node_id i`

There are optional files if the respective information is available:

* `DS_edge_labels.txt` (`m` lines; same size as `DS_A_sparse.txt`): labels for the edges in `DS_A_sparse.txt`
* `DS_edge_attributes.txt` (`m` lines; same size as `DS_A.txt`): attributes for the edges in `DS_A.txt`
* `DS_node_attributes.txt` (`n` lines): matrix of node attributes, the comma seperated values in the i-th line is the attribute vector of the node with `node_id i`
* `DS_graph_attributes.txt` (`N` lines): regression values for all graphs in the data set, the value in the i-th line is the attribute of the graph with `graph_id i`

### Deep Learning Libraries
The datasets can also be accessed using PyTorch Geometric and the Deep Graph Library.

Edit
Citing this Website
We encourage you to refer to our website at http://graphkernels.cs.tu-dortmund.de if you have used the data sets for your publication. Please use the following BibTeX citation:

@misc{KKMMN2016,
  title  = {Benchmark Data Sets for Graph Kernels},
  author = {Kristian Kersting and Nils M. Kriege and Christopher Morris and Petra Mutzel and Marion Neumann},
  year   = {2016},
  url    = {http://graphkernels.cs.tu-dortmund.de}
}
If your bibliography style does not support the url field, you may use this alternative:

@misc{KKMMN2016,
  title  = {Benchmark Data Sets for Graph Kernels},
  author = {Kristian Kersting and Nils M. Kriege and Christopher Morris and Petra Mutzel and Marion Neumann},
  year   = {2016},
  note   = {\url{http://graphkernels.cs.tu-dortmund.de}}
}
Edit
