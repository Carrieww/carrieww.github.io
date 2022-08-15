---
layout:     post
title:      Paper read "GNNExplainer - Generating Explanations for Graph Neural Networks"
subtitle:   Part of Advances in Neural Information Processing Systems 32 in 2019.
date:       2022-08-15
author:     Yun Wang
header-img: img/post8_bg.jpg
catalog: true
tags:
    - Interpretability
    - GNN
---

## Paper read "GNNExplainer - Generating Explanations for Graph Neural Networks"

[pdf](https://proceedings.neurips.cc/paper/2019/file/d80b7040b773199015de6d3b4293c8ff-Paper.pdf) is here.

This paper is by Zhitao Ying, Dylan Bourgeois, Jiaxuan You, Marinka Zitnik, Jure Leskovec. This work creates a model-agnostic approach to handle single- as well as multi-instance explanations of any GNN on any machine learning task for graphs, including node classification, link prediction, and graph classification.


### Motivation
**GNNs lack transparency as they do not easily allow for a human-intelligible explanation of their predictions.** Yet, it is important to understand GNN's predictions for
1. increasing trust in GNN model
2. improving model's transparency in the growing number of decision-critical applications pertaining to fairness, privacy and other safety challenges
3. allowing practitioners to get an understanding of the network characteristics, identify and correct systematic patterns of mistakes made by the models before deploying them in the real world.

**There are no methods for explaining GNNs, approaches explaining other types of neural networks fall into two categories.**
1. approximate local behaviors with simpler surrogate models, which are then probed for explanations.
2. carefully examine models for relevent features and find good qualitative interpretations of high level features or identify influential input instances.
However, 
1. the **saliency maps** in CNN have been shown to be misleading in some instances and prone to issues ike gradient saturation.
> A saliency map is a way to measure the spatial support of a particular class in each image. It is the oldest and most frequently used explanation method for interpreting the predictions of convolutional neural networks. The saliency map is built using gradients of the output over the input.
2. these issues are exacerbated on discrete inputs such as graph adjacency matrices because the gradient values can be very large but only on very small intervals.
3. these methods fall short in their ability to incorporate relational information provided by the graph as well as node features, the essence of graphs.
4. although recent GNN models aument interpretability via attention mechanisms (the learned edge attention values can indicate important graph structure), the values are the same for predictions across all nodes. This contradicts with many applications where an edge is essential for predicting one node but not another.

### GNNExplainer
![GeneralIdea](/img/post8_GeneralIdea.png) 
Intuitively, based on the mechanism of GNN algorithms, GNNExplainer is going to identify a small subgraph of the inputgraph together with a small subset of node features that are most influential for prediction label of a particular node. Figure 1 vividly illustrates the idea.

![INTUITION](/img/post8_Intuition.png) 
Mathematically, the key insight is the observation that the computation graph $G_c(v)$ of node $v$, which is defined by the GNN’s neighborhood-based aggregation (Figure 2), fully determines all the information the GNN uses to generate prediction $\hat{y}$ at node $v$.

#### Single-instance explanations
As the goal is to identify a subgraph $G_S \subseteq G_c$, the work formalizes the notion of importance using mutual information $MI$ and formulates the GNNExplainer as the following optimization framework:

$$\max_{G_S} MI(Y,(G_S,X_S))=H(Y)-H(Y|G=G_S,X=X_S)$$

$MI$ quantifies the change in the probability of prediction $\hat{y}=\Phi(G_c,X_c)$ when $v$’s computation graph is limited to explanation subgraph $G_S$ and its node features are limited to $X_S$. For example, consider the situation where $v_j \in G_c(v_i)$, $v_j \neq v_i$. Then, if removing $v_j$ from $G_c(v_i)$ strongly decreases the probability of prediction $\hat{y}_i$, the node $v_j$ is a good counterfactual explanation for the prediction at $v_i$.

Since the netropy term $H(Y)$ is constant because $\Phi$ is fixed for a trained GNN. The optimization problem is equivalent to minimizing conditional entropy $H(Y|G=G_S,X=X_S)$, which can be expressed as follows:

$$H(Y|G=G_S,X=X_S) = -\mathbb{E}_{Y|G_S,X_S}[\log{P_{\Phi}(Y|G=G_S,X=X_S)}]$$

Since direct optimization of the above objective function is not tractable as $G_c$ has exponentially many subgraphs. We can relax the problem by interpreting it as a variational approximation of distribution of subgraphs o$G_c$. Specifically, if we treat $G_S \sim \mathcal{G}$ as a random graph variable, the objective function becomes:

$$\min_{\mathcal{G}}\mathbb{E}_{G_S \sim \mathcal{G}}H(Y|G=G_S,X=X_S)$$

With convexity assumption, Jensen’s inequality gives the following upper bound:

$$\min_{\mathcal{G}}H(Y|G=\mathbb{E}_{\mathcal{G}}[G_S],X=X_S)$$

But in practice this assumption does not hold. However, experimentally, minimizing this objective with regularization often leads to a local minimum corresponding to high-quality explanations.

This conditional entropy can be optimized by replacing $\mathbb{E}_{\mathcal{G}}[G_S]$ by a masking of the computational graph of adjacency matrix, $A_c \otimes \sigma(M)$, where $M \in \mathbb{R}^{n \times n}$ denotes the mask that we need to learn, $\otimes$ denotes element-wise multiplication, and $\sigma$ denotes the sigmoid that maps the mask to $[0,1]^{n \times n}$.

A computationally efficient version using cross entropy and gradient descent is to focus on the following objective:

$$\min_{M}-\sum_{c=1}^C \mathbb{I}[y=c]\log{P_{\Phi}(Y=y|G=A_c \otimes \sigma(M),X=X_c)}$$

#### node feature importance selection
**Learning binary feature selector** $F$, which acts as a feature mask. The objective function becomes:

$$\max_{G_S,F}MI(Y,(G_S,F))=H(Y)-H(Y|G=G_S,X=X_S^F)$$

However, in some cases this approach ignores features that are important for prediction but take values close to zero. To address this issue we **marginalize over all feature subsets** and use a **Monte Carlo estimate** to sample from empirical marginal distribution for nodes in $X_S$ during training.

Many additional constraints are imposed on explainer.
1. regularization terms
2. encode domain-specific constraints through techniques like Larange multiplier of constraints or additional regularization lerms
3. each explanation must be a valid computation graph. e.g. explanation need to allow GNN's neural messages to flow towards node $v$ such that GNN can make prediction $\hat{y}$.

#### Multi-instance explanations through graph prototypes
To answer questions like “How did a GNN predict that a given set of nodes all have label $c$?”, a global explanation of class $c$ is needed. The goal here is to provide insight into **how the identified subgraph for a particular node relates to a graph structure that explains an entire class**.

**Algorithm**
1. for a given class $c$, first choose a reference node $v_c$ by computing the mean embedding of all nodes assigned to $c$ for example. Then, take explanation for the reference node and align it to explanations of other nodes assigned to class $c$.
2. aggregate aligned adjacency matrices into a graph prototype $A_{text{proto}}$ using, for instance, a robust median-based approach. $A_{text{proto}}$ gives insights into graph patterns shared between nodes within the same class. One can then study patterns.


### reference
> 1. https://proceedings.neurips.cc/paper/2019/file/d80b7040b773199015de6d3b4293c8ff-Paper.pdf