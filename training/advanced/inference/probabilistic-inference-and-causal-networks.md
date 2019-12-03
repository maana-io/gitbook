---
description: >-
  Use Bayesian theory to learn to perform a reasoning task using the Q AI
  Simulator framework.
---

# Probabilistic Inference and Causal Networks

### Initial Network

The structure of our taxicab network might initially look something like this. This says that `Location`, `hasPassenger` and `Action` are all discrete distributions, and that we believe _a priori_ that probabilities location and action may be conditional upon the value fo `hasPassenger`.

![](../../../.gitbook/assets/screen-shot-2019-12-03-at-7.17.59-am.png)

## Learning

Updates of Bayesian networks is an online learning rather than batch training/update method. The agent has prior distributions for the conditional probabilities of states and actions and can learn incrementally as it observes actual behavior of the simulation \(i.e., consequences of taking actions in various states\).

Imagine at each time step you are presented with a new collection of observations for what the correct action to be taken is. This knowledge can be used to incrementally adapt the network structure or of the conditional probabilities \(via MLE or Bayesian arithmetic\), \([https://arxiv.org/pdf/1302.1538.pdf](https://arxiv.org/pdf/1302.1538.pdf)\).  This is referred to as _structural learning_ vs _parameter learning_, respectively, and will be discussed below.

### Structural Learning

For _structural learning_, we expect that over time, we learn that `Location` and `hasPassenger` are independent \(i.e., not connected\):

![](../../../.gitbook/assets/screen-shot-2019-12-03-at-7.35.03-am.png)

### Parameter Learning

For _parameter learning_, we would expect that we would eventually learn that:

$$
P( Action = DropOff | Location = atDropOff, hasPassenger = T ) = 100\%
$$

$$
P( Action = Pickup  | Location = atPickup, hasPassenger = F ) = 100\%
$$

$$
P( Action = Move | Location = atOther ) = 100\%
$$

For more information, please see "[Update rules for parameter estimation in Bayesian networks](https://arxiv.org/pdf/1302.1519.pdf)" and "[Parameter Estimation in Bayesian Networks](https://courses.cs.ut.ee/2009/bayesian-networks/orasmaa-liin-chapter-6.pdf)."

