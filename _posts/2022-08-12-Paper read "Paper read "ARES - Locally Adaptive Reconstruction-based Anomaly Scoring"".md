---
layout:     post
title:      Paper read "ARES - Locally Adaptive Reconstruction-based Anomaly Scoring"
subtitle:   ArXiv preprint in 2022.
date:       2022-08-12
author:     Yun Wang
header-img: img/post5_bg.jpg
catalog: true
tags:
    - Anomaly Detection
    - Unsupervised Learning
---

## Paper read "ARES - Locally Adaptive Reconstruction-based Anomaly Scoring"

[pdf](https://arxiv.org/pdf/2206.07604.pdf) is here.

This paper is by Adam Goodge, Bryan Hooi, See Kiong Ng, Wee Siong Ng. The work has two contributions. One is to identify the problem that anomaly detection required neighboring information so that local adaptivity is needed. The second is to use ARES, a scoring method, to detect anomalies.

### Bacground Knowledge
#### Conventional anomaly score
In standard approach, residual $\epsilon=x-\hat{x}$, the anomaly score is 

$$R(\epsilon) := \|\epsilon\|^2_2 = \|x-\hat{x}\|^2_2$$

Assume $\epsilon$ follows a Gaussian distribution with zero meana and unit variance: $\epsilon \sim \mathcal{N}(0,\mathbf{I})$

$$P(\epsilon) = \frac{1}{\sqrt{2 \pi}} e^{\frac{-\|x\|^2}{2}}$$

$$-\log P(\epsilon)=\frac{d}{2}\log{(2\pi)}+\frac{R(\epsilon)}{2}$$

The negative log-likelihood is an intuitive anomaly score because anomalous samples should have lower likelihood, thus higher negative log-likelihood.

#### What is LOF
**Local Outlier Factor (LOF)** is a score that tells how likely a certain data point is an outlier/anomaly.

LOF ≈ 1 ⇒ no outlier
LOF ≫ 1 ⇒ outlier

The LOF is a calculation that looks at the neighbors of a certain point to find out its density and compare this to the density of other points later on. It tells the density of this point compared to the density of its neighbors. If the density of a point is much smaller than the densities of its neighbors (LOF ≫1), the point is far from dense areas and, hence, an outlier.

### Motivation
Because of the difficulty of obtaining accurate labels of anomalous data, unsupervised methods are used to learn the distribution of an **all-normal training set**. Anomaly scores are important measurement of anomalies. The reconstruction error can be directly used as anomaly score. However, this anomaly score fails to account for the fact that reconstruction error can vary greatly even amongst different types of normal samples. For example, weekday sensor samples and weekend ones have different distributions but they are all regarded as normal samples.

Conventional reconstruction error with the same error threshold invokes the implicit assumption that the reconstruction errors of all samples are identically distributed, regardless of any individual characteristics and context which could potentially influence the reconstruction error significantly.

### Contribution:

1. Empirically show with real,multi-class data the variation in reconstruction error among different samples in the normal set and why this justifies the need for local adaptivity in anomaly scoring.
2. Propose a novel anomaly scoring method, **Adaptive Reconstruction Error-based Scoring (ARES)**, which adapts to this variation by evaluating anomaly status based on the local context of a given sample in the latent space.

### Methodology
#### Demostrate homoscedasticity assumption is invalid

![MNIST](/img/post5_MNIST.png)  
1. **Inter-class valriation:** Within the normal set, we can observe separate classes. The class label can be seen as a variable characteristic between different samples.
2. **Intra-class variation:** Within any single cluster, there is significant variation. Therefore there are noticeably distinct regions of high and low reconstruction errors within each individual cluster. Hence, there exists additional characteristics which influence whether a given normal sample has a high or low reconstruction error besides class label.

![NeighborhoodError](/img/post5_NeighborhoodError.png)  
3. **Neighborhood correlation:** The variance in test errors increases for larger neighbourhood errors: a clear heteroscedastic relationship. This information is useful in determining anomalousness: a test error of 0.1 would be anomalously high if its neighbourhood error is 0.02, but normal if it is 0.06.

Therefore, ARES aims to address flaw (a fixed Gaussian with constant mean and variance is inapproriate) by adapting the coring for each samples local context in the latent space.

#### ARES
ARES is based on joint-likelihood of a samples residual $\epsilon$ with its latent encoding $z$, defined as follows:

$$-\log{P(\epsilon,z)}=-\log{P(\epsilon|z)}-log{P(z)}$$

The former part is called **Local Reconstruction Score**, while the later part is called **Local Density Score**.

##### Local Reconstruction Score
The local reconstruction score is based on an estimate of how likely a given residual $\epsilon$ (and consequent reconstruction error) is to come from the corresponding sample $x$, based on its latent encoding $z$:

$$r(x)=-\log P(\epsilon|z)$$

However, given $z$, we cannot calculate the likelihood. Instead, we consider the $k$ nearest neighbors of $z$ in the latent space, denoted $N_k(z)$ to represent the sample population which $z$ belongs to.

The idea is to measure the difference between the test points reconstruction error and the median reconstruction error of its neighboring samples. (For testing samples $x$, we still find its neighbours in training set.) The median is used because it was found to perform better than the mean as it is more robust to extrema. The larger the difference between them, the more outlying the test point is in comparison to its local neighbours, therefore the more likely it is to be anomalous. Therefore, the local reconstruction score is:
$$r(x)=\|x-\hat{x}\|^2_2-\text{median}_{\mathbf{n} \in N_k(z)}(\|\mathbf{n}-\mathbf{\hat{n}}\|^2_2)$$

![Algo](/img/post5_Algo.png)  

#### Local Density Score
The local density score is the likelihood of observing the given encoding in the latent space. Any multivariate distribution P, with trainable parameters Θ, could be used to estimate this density:

$$d(x)=-\log{P(z;\Theta)}$$

The distribution $P$ need not be normalized. As LOF is an unnormalized score which is similarly locally adaptive, this paper uses LOF in experiments to calculate local density score.

Hence, the overall anomaly score for sample $x$ is;
$$s(x)=r(x)+\alpha d(x)$$

where $\alpha$ is used to balance the relative magnitudes of the two scores.

### reference
> 1. https://arxiv.org/pdf/2206.07604.pdf
> 2. https://towardsdatascience.com/local-outlier-factor-for-anomaly-detection-cc0c770d2ebe