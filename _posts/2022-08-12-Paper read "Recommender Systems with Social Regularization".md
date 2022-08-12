---
layout:     post
title:      Paper read "Recommender Systems with Social Regularization"
subtitle:   Proceedings of the fourth ACM international conference on Web search and data mining in 2011.
date:       2022-08-012
author:     Yun Wang
header-img: img/post3_bg.jpg
catalog: true
tags:
    - Recommender Systems
    - Social Regularization
---

## Paper read "Recommender Systems with Social Regularization"

[pdf](https://www.microsoft.com/en-us/research/wp-content/uploads/2011/01/wsdm10.pdf) is here.

This paper is by Hao Ma, Dengyong Zhou, Chao Liu, Michael R Lyu, Irwin King. The work is to improve recommender system by incorporating social network information using matrix factorization framework with social regularization.

### What is Social Recommender Systems?
Using social friends network to address/improve recommender systems problem. A recommender system problem refers to effectively and efficiently predict the missing values of the user-item matrix.

### Motivation
1. **Traditional recommender system (collaborative filtering)** always ignore social relationships among users, based on the assumption that users are independent and identically distributed. While in real life, we always ask friends for recommendations. Hence, to improve recommender systems and to provide more personalized recommendation results, incorporating social network information among users are necessary.
2. **Trust-aware recommendation methods**, using inferred implicit or explicit trust information, to improve traditional recommender systems have limitations and weakness:
    1. The process of trust generation is **unilateral**, A likes a review issued by B implies A will add B to his/her trust list while B may not even know A. Thus, trust relationships are different from social friendships.
    2. Trust-aware recommender systems are based on the assumption that u**sers have similar tastes with other users they trust**. This may not be true in social recommender systems because friends may not share the same interests all the time.

### Contribution:

1. Elaborate how social network information can benefit recommender systems
2. Interpret the differences between social-based recommender systems and trust-aware recommender systems
3. Systematically illustrate with social regularization
4. Proposed a general method, which can be easily extended to incorporate other contextual information, like social tags, etc.

### Methodology
#### Model 1: Average-based regularization
Traditionally, the Singular Value Decomposition (SVD) is to approximate low-rank user and item matrix by minimizing:

$\mathcal{L} = \displaystyle \min_{{U,V}} \frac{1}{2}\|\mathcal{R}-{U}^T{V}\|_F^2$

However, due to the reason that $\mathcal{R}$ contains a large number of missing values, we only need to factorize the observed ratings in matrix $\mathcal{R}$, hence the loss function becomes:

$\mathcal{L} = \displaystyle \min_{{U,V}} \frac{1}{2} \sum_{i=1}^m \sum_{j=1}^n \mathcal{I}_{ij} (\mathcal{R}_{ij}-{U}_i^T{V}_j)^2$

To avoid overfitting, we add regularization terms:

$\mathcal{L} = \displaystyle \min_{{U,V}} \frac{1}{2} \sum_{i=1}^m \sum_{j=1}^n \mathcal{I}_{ij} (\mathcal{R}_{ij}-{U}_i^T{V}_j)^2 + \frac{\lambda_1}{2}\|{U}\|_F^2 + {\lambda_2}{2}\|{V}\|_F^2$

The optimization problem here minimizes the sum-of-squared-errors objective function with quadratic regularization terms.

Then, based on the assumption that users are affected differently by their friends based on how similar they are. Similar friends will contribute their attributes more to your attributes, while dissimilar friends will contribute less. The loss function is modified to:

$\mathcal{L} = \displaystyle \min_{{U,V}} \frac{1}{2} \sum_{i=1}^m \sum_{j=1}^n \mathcal{I}_{ij} (\mathcal{R}_{ij}-{U}_i^T{V}_j)^2 + \frac{\alpha}{2} \sum_{i=1}^m\|{U}_i-\frac{\sum_{f\in\mathcal{F}^+_{i} Sim(i,f)\times {U}_f}}{\sum_{f\in\mathcal{F}^+_{i} Sim(i,f)}}\| + \frac{\lambda_1}{2}\|{U}\|_F^2 + \frac{\lambda_2}{2}\|{V}\|_F^2$

where $\alpha > 0$, $\mathcal{F}^+_i$ is the set of friends of user $u_i$, more specifically, $u_i$'s outlink friends. $u_i$'s inlink friends is represented by $\mathcal{F}^-_i$. $Sim(i,f) \in [0,1]$ is the similarity function to indicate the similarity between $u_i$ and $u_f$. A local minimum of this objective function can be found by performing fradient descent in freature vectors $U_i$ and $V_j$.

#### Model 2: Individual-based Regularization
However, the above approach is insensitive to those users whose friends have diverse tastes. Because we sum up all friends' attributes with weight being their similarities, if similarity is very diverse, summing up will loss individual information. Therefore, another regularization term can be:

$\mathcal{L}_2 = \displaystyle \min_{{U,V}} \frac{\beta}{2}\sum_{i=1}^m \sum_{f\in\mathcal{F}^+_i} Sim(i,f) \|U_i-U_j\|_F^2$

in which a small value of $Sim(i,f)$ indicates that the distance between feature vectors $U_i$ and $U_f$ should be larger, while a large value tells that the diatnce should be smaller. Therefore, the second social recommendation model can be formulated as:

$\mathcal{L}_2 = \displaystyle \min_{{U,V}} \frac{1}{2} \sum_{i=1}^m \sum_{j=1}^n \mathcal{I}_{ij} (\mathcal{R}_{ij}-{U}_i^T{V}_j)^2 + \frac{\beta}{2}\sum_{i=1}^m \sum_{f\in\mathcal{F}^+_i} Sim(i,f) \|U_i-U_j\|_F^2 + \frac{\lambda_1}{2}\|{U}\|_F^2 + {\lambda_2}{2}\|{V}\|_F^2$

Another advantage of this approach is that it indirectly models the propagation of tastes. If $u_i$ is closer to $u_j$ and $u_j$ is closer to $u_k$, even though $u_i$ and $u_k$ are not friends, we actually indirectly minimize the distance between feature vectors $U_i$ and $U_k$.

### Experiment results
Among two models, the second model outperforms the first model. Also, different similarity functions, such as Pearson Correlation Coefficient (PCC) based and Vector Space Similarity (VSS) based similarity. Empirical results show that PCC-based similarity function can better capture similarities between two users.

### Future work
1. only constrain user feature vectors while ignoring the item side. If there exists correlations between the items, we can also incorporate item regularization terms to further improve prediction accuracy.
2. develop similar techniques to allow one user’s friends to influence this user’s search results, query suggestions.

### reference
> 1. https://www.microsoft.com/en-us/research/wp-content/uploads/2011/01/wsdm10.pdf