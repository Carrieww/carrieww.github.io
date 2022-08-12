---
layout:     post
title:      Paper read "CenGCN - Centralized Convolutional Networks with Vertex Imbalance for Scale-Free Graphs"
subtitle:   A paper in IEEE 2022.
date:       2022-08-07
author:     Yun Wang
header-img: img/post2_bg.jpg
catalog: true
tags:
    - GCN
    - Vertex Imbalance
    - Scale-Free Graphs
---

## Paper read "CenGCN - Centralized Convolutional Networks with Vertex Imbalance for Scale-Free Graphs"

[pdf](https://arxiv.org/pdf/2202.07826.pdf) is here.

This paper is by Feng Xia, Lei Wang, Tao Tang, Xin Chen, Xiangjie Kong, Giles Oatley, and Irwin King. The work is to study the vertex imbalance problem in scale-free graphs using centrality, random ralk similarity, and hub attention mechanism on conventional GCN.

### Background
**Centralized or Scale Free or Power-law Networks:** 
power/exponential relationship between the degree of connectivity a node has and the frequency of its occurrence.

> Number of nodes with degree x is proportional to 1/x^2

Use cases: citation of academic papers, within social networks, molecules hubs in metabolic networks,  networks

### Contribution:

1. CenGCN for scale-free networks, addressing the unequal importance of information from different vertices
2. Label propagation to quantify the similarity between hub vertices and their neighbor; a graph transformation method to capture the influence of hub vertices by vertex centrality;  a hub attention mechanism that assign new weights to non-hub neighbors shared by the same hubs.
3. Two variants of CenGCN, CenGCN_D and CenGCN_E, representing degree centrality and eigenvalue centrality. 

### Methodology
#### Framework
![framework](/img/post2_CenGCN_Framework.png)  

**Steps:**
1. Compute the vertex centrality indices, and identify hub vertices.
2. Using random walk, or namely label propagation method, to quantify the similarity between hubs and their neighbors.
3. Using the quantified similarities and centrality indices, we transform the given graph to a new graph by increasing or decreasing the weight of each edge.
4. Multi-layer GCN with hub attention mechanism

![transformedA](/img/post2_CenGCN_TransformedA.png)
The above screenshot shows how the transformed adjacency matrix is defined to incorporate vertex centrality and consider the influence of hub vertices on their dissimilar neighbors.

### Future works
Despite their prevalence, GCNs suffer from local limits and shallow models. It is worth trying to consider more network characteristics, such as subgraphs, to enhance and enrich GCNs.

### reference
> 1. https://arxiv.org/pdf/2202.07826.pdf 