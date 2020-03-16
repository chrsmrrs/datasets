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

#### Citing this Website
We encourage you to refer to our website at https://chrsmrrs.github.io/datasets/docs/home/ if you have used the data sets for your publication. Please use the following BibTeX citation:

```
@misc{KKMMN2016,
  title  = {Benchmark Data Sets for Graph Kernels},
  author = {Kristian Kersting and Nils M. Kriege and Christopher Morris and Petra Mutzel and Marion Neumann},
  year   = {2016},
  url    = {http://graphkernels.cs.tu-dortmund.de}
}
```

If your bibliography style does not support the url field, you may use this alternative:

```
@misc{KKMMN2016,
  title  = {Benchmark Data Sets for Graph Kernels},
  author = {Kristian Kersting and Nils M. Kriege and Christopher Morris and Petra Mutzel and Marion Neumann},
  year   = {2016},
  note   = {\url{http://graphkernels.cs.tu-dortmund.de}}
}
```

### Bibliography

[1] Debnath, A.K., Lopez de Compadre, R.L., Debnath, G., Shusterman, A.J., and Hansch, C. Structure-activity relationship of mutagenic aromatic and heteroaromatic nitro compounds. Correlation with molecular orbital energies and hydrophobicity. J. Med. Chem. 34(2):786-797 (1991).

[2] Helma, C., King, R. D., Kramer, S., and Srinivasan, A. The Predictive Toxicology Challenge 2000–2001. Bioinformatics, 2001, 17, 107-108. URL: www.predictive-toxicology.org/ptc

[3] Feragen, A., Kasenburg, N., Petersen, J., de Bruijne, M., Borgwardt, K.M.: Scalable kernels for graphs with continuous attributes. In: C.J.C. Burges, L. Bottou, Z. Ghahramani, K.Q. Weinberger (eds.) NIPS, pp. 216-224 (2013).

[4] K. M. Borgwardt, C. S. Ong, S. Schoenauer, S. V. N. Vishwanathan, A. J. Smola, and H. P. Kriegel. Protein function prediction via graph kernels. Bioinformatics, 21(Suppl 1):i47–i56, Jun 2005.

[5] I. Schomburg, A. Chang, C. Ebeling, M. Gremse, C. Heldt, G. Huhn, and D. Schomburg. Brenda, the enzyme database: updates and major new developments. Nucleic Acids Research, 32D:431–433, 2004.

[6] P. D. Dobson and A. J. Doig. Distinguishing enzyme structures from non-enzymes without alignments. J. Mol. Biol., 330(4):771–783, Jul 2003.

[7] Sutherland, J. J.; O'Brien, L. A. & Weaver, D. F. Spline-fitting with a genetic algorithm: a method for developing classification structure-activity relationships. J. Chem. Inf. Comput. Sci., 2003, 43, 1906-1915.

[8] N. Wale and G. Karypis. Comparison of descriptor spaces for chemical compound retrieval and classification. In Proc. of ICDM, pages 678–689, Hong Kong, 2006.

[9] http://pubchem.ncbi.nlm.nih.gov

[10] http://image.diku.dk/aasa/papers/graphkernels_nips_erratum.pdf

[11] M. Neumann, P. Moreno, L. Antanas, R. Garnett, K. Kersting. Graph Kernels for Object Category Prediction in Task-Dependent Robot Grasping. Eleventh Workshop on Mining and Learning with Graphs (MLG-13), Chicago, Illinois, USA, 2013.

[12] http://www.first-mm.eu/data.html

[13] M. Neumann, R. Garnett, C. Bauckhage, and K. Kersting. Propagation kernels: efficient graph kernels from propagated information.Machine Learning, 102(2):209–245, 2016

[14] Pinar Yanardag and S.V.N. Vishwanathan. 2015. Deep Graph Kernels. In Proceedings of the 21th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, ACM, New York, NY, USA, 1365-1374.

[15] Francesco Orsini, Paolo Frasconi, and Luc De Raedt. 2015 Graph invariant kernels. In Proceedings of the 24th International Conference on Artificial Intelligence (IJCAI'15), Qiang Yang and Michael Wooldridge (Eds.). AAAI Press 3756-3762.

[16] Riesen, K. and Bunke, H.: IAM Graph Database Repository for Graph Based Pattern Recognition and Machine Learning. In: da Vitora Lobo, N. et al. (Eds.), SSPR&SPR 2008, LNCS, vol. 5342, pp. 287-297, 2008.

[17] AIDS Antiviral Screen Data (2004)

[18] S. A. Nene, S. K. Nayar and H. Murase. Columbia Object Image Library (COIL-100), Technical Report, Department of Computer Science, Columbia University CUCS-006-96, Feb. 1996.

[19] NIST Special Database 4

[20] Jeroen Kazius, Ross McGuire and, and Roberta Bursi. Derivation and Validation of Toxicophores for Mutagenicity Prediction, Journal of Medicinal Chemistry 2005 48 (1), 312-320

[21] Christopher Morris, Nils M. Kriege, Kristian Kersting, Petra Mutzel. Faster Kernels for Graphs with Continuous Attributes via Hashing, IEEE International Conference on Data Mining (ICDM) 2016

[22] Nino Shervashidze, Pascal Schweitzer, Erik Jan van Leeuwen, Kurt Mehlhorn, and Karsten M. Borgwardt. 2011. Weisfeiler-Lehman Graph Kernels. J. Mach. Learn. Res. 12 (November 2011), 2539-2561.

[23] Nils Kriege, Petra Mutzel. 2012. Subgraph Matching Kernels for Attributed Graphs. International Conference on Machine Learning 2012.

[24] Tox21 Data Challenge 2014

[25] Nils M. Kriege, Matthias Fey, Denis Fisseler, Petra Mutzel, Frank Weichert. Recognizing Cuneiform Signs Using Graph Based Methods. International Workshop on Cost-Sensitive Learning (COST), SIAM International Conference on Data Mining (SDM) 2018, 31-44, arXiv:1802.05908.

[26] A Repository of Benchmark Graph Datasets for Graph Classification

[27] Boris Knyazev, Graham W. Taylor, Mohamed R. Amer. Understanding Attention and Generalization in Graph Neural Networks

[28] Chemical DataSets

[29] Alchemy: A Quantum Chemistry Dataset for Benchmarking AI Models


