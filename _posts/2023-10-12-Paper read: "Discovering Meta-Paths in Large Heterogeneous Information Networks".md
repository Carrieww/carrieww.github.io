---
layout: post
title: Paper read "Discovering Meta-Paths in Large Heterogeneous Information Networks"
subtitle: A paper in WWW 2015.
date: 2023-10-12
author: Yun Wang
header-img: img/post9_bg.jpg
catalog: true
tags:
  - HINs
  - Meta-Paths
---

## Paper read: "Discovering Meta-Paths in Large Heterogeneous Information Networks"

[pdf](https://reynold01.github.io/hkucs-homepage/papers/www15-metapath.pdf) is here.

This paper is by Changping Meng, Reynold Cheng and other researchers. The work is to study autonomous generation of
meta-paths from HINs.

### Literature Review on Meta-Paths Generation

Although meta-paths are useful in many real-world applications, the important issue of how to generate meta-paths has
not been well studied. Most existing work assumes that meta-paths are provided by domain experts, which may not be
feasible for larger HINs. The only meta-path generation solution is proposed in [10], yielding meta-paths within a fixed
length $l$.

### Contribution

1. The paper discusses the importance of meta-paths in heterogeneous information networks (HINs), in tasks such as
   information retrieval, decision-making, and product recommendation.
2. The paper proposes a two-phase greedy algorithm for automatically generating meta-paths, making the process less
   manual and more efficient.
3. The paper performs experiments on DBLP and Yago, showing the effectiveness, efficiency, and how it can improve expert
   meta-paths. It also includes a comprehensive study on the impact of varying input size, class label, $\alpha$. A user
   study is performed to determine whether meta-paths learned by Forward Stagewise Path Generation (`FSPG`) are of
   interest to users.

### Methodology

#### Phase I: Link-Only Path Generation

![framework](/img/20231012_meta_path_algo1.png)

This phase generates meta-paths with only edge types, by using Forward Stagewise Path Generation (`FSPG`). The model is
a regression model trained based on a modified version of the Least-Angle Regression (`LARS`)

1. Initialize the model with the first meta-path found by the greedy algorithm, which I will explain in detail later.
2. Then, at each stage, the model will test the next meta-path, by computing its correlation to the currently
   constructed model (same as the selection criterion for choosing features in `LARS`). Each time the model will choose
   the meta-path with the largest correlation with the current residual based on a standard cosine similarity. Residual
   value is a vector, denoting the difference between the values of the ground truth examples (positive or negative
   input pairs indicated by the input) and the model result (positive or negative input pairs indicated by the current
   model).

> Note that the author generates negative samples by Lowest Common Ancestor (`LCA`) according to the class hierarchy
> rather than random draws to control false negative pairs.

As shown in the above algorithm, $X$ is a feature matrix where each column represent a vector of similarity scores for
different input pairs (both positive and negative) given a meta-path. The similarity function used in the paper is a
generalized version of Path Count (`PC`) and Path-Constrained Random Walk (`PCRW`), which is called Biased Path
Constrained Random Walk (`BPCRW`).

#### GreedyTree Structure

![framework](/img/20231012_meta_path_fig4.png)

Next, we talk about how the author fins the meta-path $m_k$ with the largest correlation with the `GreedyTree`
algorithm. The algorithm works by expanding a tree structure where each tree edge stores the edge type and each tree
node stores a list of node pairs with BPCRW values and a priority score $S$. The priority score heuristically indicates
the possibility of reaching the highest BPCRW along the expansion. As shown in Figure 4, the algorithm first initiate
the pair by the starting nodes of input pairs. Then the tree generates three leaf nodes because the graph contains three
types of edges, implying three possible routes for expansion. By calculating the BPCRW and priority scores, the tree
further expands through the leaf with the highest priority score.

You may also check the algorithm below:

![framework](/img/20231012_meta_path_algo2.png)

#### Phase II: Node CLass Generation

Based on Phase I and the `GreedyTree` algorithm, we can obtain meta-paths with only edge types. Phase II is to generate
the node types in those generated meta-paths. Why we cannot just use link-only meta-paths? It is because they are less
specific to input pairs, hence impairing the result quality.

The node types or classes are chosen by referring to the `LCA` in a tf-idf manner. How does it work? For instance, in
the first node of the `Greedytree` algorithm in Figure 4, $tf$(USPresident) is 2 since it contains 1 and 3. On the other
hand, $of$(USPresident) is 42, since there are 42 nodes with label USPresident in the entire Knowledge Base. Then the
score of USPresident is $\frac{2}{log(42)}=1.23$, which is higher than other labels for these example nodes. In summary,
when we get meta-paths from greedy algorithm, we calculate for each node position in the paths, the tf-idf score, to
calculate what class is possible for this position of node. In our example, we have two meta-paths generated and both of
them start with USPresident type, so that the first node should be USPresident.

> It is worth noting that $of$ can be precomputed as a pre-processing step.

### reference

> 1. https://reynold01.github.io/hkucs-homepage/papers/www15-metapath.pdf