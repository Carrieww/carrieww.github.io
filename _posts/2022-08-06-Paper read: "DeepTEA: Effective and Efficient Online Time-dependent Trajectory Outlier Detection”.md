---
layout:     post
title:      Paper read "DeepTEA - Effective and Efficient Online Time-dependent Trajectory Outlier Detection"
subtitle:   A paper In PVLDB 2022.
date:       2022-08-03
author:     Yun Wang
header-img: img/traffic.jpg
catalog: true
tags:
    - Urban Computing
    - Trajectory Outlier Detection
    - CNN
    - RNN
---

## Paper read: "DeepTEA: Effective and Efficient Online Time-dependent Trajectory Outlier Detection"

This paper is by Xiaolin Han, Reynold Cheng, Chenhao Ma, Tobias Grubenmann from HKU and University of Bonn. The work is to study anomalous trajectory detection, which aims to extract abnormal movements of vehicles on the roads. 

### Literature Review 
**Shape-based trajectory outlier solutions:** judge outlier by shape of routes.

However, **trajectory outliers are time-dependent**. The problem is it does not consider the fact that outliers can change over time. (e.g. congested road forces vehicles to switch to another usually-less-popular route.)

Time-dependent solutions are few, all considering different factors that affect the time-dependent normal routes, e.g. incidents, roadblocks, rush hours. Then use distance to judge if a route is an outlier. However, the problems are: 

1. Find a good threshold is hard but essential
2. High time complexity, cannot be used in online outlier detection.


### Contribution  
1. develop an effective time-dependent outlier detection. using deep probabilistic neural network  to get latent traffic pattern for classifying smooth or congested road.
2. Improve efficiency to allow companies or passengers to be alerted online by abnormal driving behaviors during a journey. Use generative network based on latent traffic pattern to generate the observed trajectories. If cannot generate one path, then this path is a time-dependent outlier.

### Methodology
#### Latent Traffic Pattern Inference
Given Z_{ti}, which is an average speed matrix covering the moving condition of the whole city at ti, we perform CNN on it, to alleviate traffic scarcity issue and get latent representation of each area in a city at ti
Then, we perform RNN on the time series of latent representations of the whole city to learn traffic transition as time changes. The set of parameters in RNN is used to capture latent traffic pattern z

#### Latent Time-dependent Route Inference
**Inference network: to infer latent time-dependent route r from observations o(p_{ti},z) of trajectory T**
Given trajectory T, we not only know location p_{ti}, but also the latent traffic pattern z. Therefore, given T, we can infer latent time-dependent route r, route type k, Latent traffic pattern z through a inference network.

#### Trajectory Observation Generation
Based on inferred latent time-dependent route r, route type k, and latent traffic pattern z, maximize the probability of generating trajectory observation o(p_{ti},z), which is position and latent traffic pattern z.


### reference
> 1. https://www.vldb.org/pvldb/vol15/p1493-han.pdf 