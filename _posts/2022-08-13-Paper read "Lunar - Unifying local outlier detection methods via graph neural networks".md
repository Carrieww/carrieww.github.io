---
layout:     post
title:      Paper read "Lunar - Unifying local outlier detection methods via graph neural networks"
subtitle:   Proceedings of the AAAI Conference on Artificial Intelligence in 2022.
date:       2022-08-13
author:     Yun Wang
header-img: img/post6_bg_new.jpg
catalog: true
tags:
    - GNN
    - Anomaly Detection
    - Unsupervised Learning
---

## Paper read "Lunar - Unifying local outlier detection methods via graph neural networks"

[pdf](https://ojs.aaai.org/index.php/AAAI/article/view/20629) is here.

This paper is by Adam Goodge, Bryan Hooi, See-Kiong Ng, Wee Siong Ng. The work generalized local outlier methods based on message passing scheme used in GNN and address the following two problems with local outlier detection methods using GCN:
1. Distance-based outlier detection methods cannot optimize or adapt to a particular set of data through trainable parameters.
2. In an unsupervised setting, it is hard to find optimal nearest neighbors, which is extremely important and greatly affect the performance of Distance-based outlier detection methods.

### Motivation
The two motivations are shown above.

### Contribution:

1. Generalize local outlier methods under a simple, general framework based on the message passing scheme used in GNN
2. Address the above two issues with local outlier detection methods using GCN

### Methodology
#### Unifying Framework
Local outlier detection methods 	can be represented by message-passing GNN. E.g. KNN (every node connects to its k-nearest neighbors, and distance information are passed to target node. Aggregation function outputs the maximum of these distances, and update function outputs the result as an anomaly score.)

#### LUNAR
Local Outlier Detection Methods via Graph Neural Networks
Algorithm:
1. Construct k-NN graph (each node connects to its k-nearest neighbors according to distance)
2. Distance is stored on edges and passed during message-passing stage
3. Use a learnable aggregation because of the fixed number of neighbors. Concatenating collected messages to give a k-dimensional vector. Pass it to a neural network to output a single, scalar value representing the anomalousness of node i
4. Output the learned aggregated message in update stage.

**Negative sampling** is to create some negative samples in the training set.
Negative samples have been used to introduce supervision to unsupervised tasks, such as contrastive learning and anomaly detection.

### Limitation
The core idea of LUNAR is still find the k-nearest neighbors. Since in high-dimensional spaces, such as in an image, the distance between two images does not have meaningful implications. Therefore, in these cases, methods based on k-nearest neighbors are inappropriate.

### reference
> 1. https://ojs.aaai.org/index.php/AAAI/article/view/20629