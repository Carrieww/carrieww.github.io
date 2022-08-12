---
layout:     post
title:      Paper read "Where You Like to Go Next - Successive Point-of-Interest Recommendation"
subtitle:   Conference paper at Twenty-Third international joint conference on Artificial Intelligence in 2013.
date:       2022-08-12
author:     Yun Wang
header-img: img/post4_bg.jpg
catalog: true
tags:
    - Recommender Systems
    - POI recommendation
    - LBSN
---

## Paper read "Where You Like to Go Next - Successive Point-of-Interest Recommendation"

[pdf](https://www.ijcai.org/Proceedings/13/Papers/384.pdf) is here.

This paper is by Chen Cheng, Haiqin Yang, Michael R Lyu, Irwin King. Based on the current work FPMC, this work improves the POI recommendation by incorporating localized region constraint. More importantly, utilizing the information of localized regions, we not only reduce the computation cost largely, but also discard the noisy information to boost recommendation.

### Background
#### What is Point of Interest?
A **point of interest** (abbreviated POI) is a specific place or location point on a map that someone might find interesting or useful. It can be a restaurant, a hotel or a tourist attraction, or it can be ordinary places like ATMs, gas stations, schools or parks. A point of interest can be temporary such as an event, or it can be permanent such as a building or even a city. 

#### What is Check-in Behavior?
俗称“打卡”

#### What is LBSN?
Location-based social networks

### Motivation
1. Based on **GPS trahectory logs** (usually small number of users, butdense records), many collaborative filtering algorithms, deeming the locations as items, have been proposed to solve the task of PIO recommendation.
2. Based on **LBSN data** (very sparse and large-scale), many methods are explored to address the problem.

However, the temporal relation between successive check-ins is not well-studied. Existing related works only use temporal information on POI preiction or next place predcition based on the existing locations or users' hidtorical trajectories.

### Contribution:

1. We formally define the problem of successive personalized POI recommendation in LBSNs and analyze the spatial-temporal properties in two large-scale real-world LBSN datasets, Foursquare and Gowalla. After analyzing the dynamics of new POIs and inter check-ins, we observe two important properties: personalized Markov chain and localized region constraint. 
2. We propose a novel matrix factorization method, namely FPMC-LR, to incorporate these two properties. More importantly, we not only reduce the computation cost largely, but also discard noisy information.

### Successive POI Recommendation in LBSNs
#### Problem statement
Given a sequence of check-ins, $\mathcal{L}^1_u$,...,$\mathcal{L}^t_u$, the latitude and longitude of each location, the problem of successive personalized POI recommendation is to provide the most suitable recommendation for user $u$ at time $t+1$.
#### New POI Dynamics and Inter Check-in Dynamics
**New POI Dynamics:**
New POIs are locations that a user does not visit before and will be recommended in the next time stamp. **New POI Dynamics** report cumulatively the amount of users who would like to explore new POIs timewise and distancewise. e.g. 70% and 80% *users* of Foursquare and Gowalla, respectively, would like to checi-in a new POI ofer 100 hours.

**Inter Check-in Dynamics:**
It reports how often successive check-ins occurs timewise and distancewise e.g. 40% and 40% *successive check-ins* occur in Foursquare and Govalla, respectively within two hours. 

Apart from timewise results, they all show that successive check-ins are influenced by geographical constraints. From New POI Dynamics, users' exploration on new POIs is restricted by the geographical influence. From Inter Check-in Dynamics, most users’ inter check-ins occur within a specific area they live or the long distance inter check-ins imply an occasional journey. 

### Factorized Personalized Markov Chains (FPMC) with Localized Region Constraint
#### Model
Leveraging work donw by Rendle et al. 2010 on FPMC, this paper only focuses on the localized region constraint. [to be continued]


### reference
> 1. https://www.plotprojects.com/blog/points-of-interest-poi-data-guide/
> 2. https://www.ijcai.org/Proceedings/13/Papers/384.pdf