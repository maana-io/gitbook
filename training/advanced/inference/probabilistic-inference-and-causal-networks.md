---
description: >-
  Use Bayesian theory to learn to perform a reasoning task using the Q AI
  Simulator framework.
---

# Probabilistic Inference and Causal Networks

## Overview

Bayesian networks \(belief networks, decision networks\) are compact graphical representations of the observables of a system and the probabilistic relationships between them. Bayesian networks, and can be used to answer stochastic questions about unobserved variables \( e.g. Given that it is January, and without knowledge of whether the sprinklers ran or if it rained, what is the likelihood that the grass is wet?" \).

Inference over Bayesian networks can be used to simulate more realistic random behavior by conditionally predicting the action to take in response to observed variables. This can be coupled with either batch or inline machine learning to provide predictions that improve over time.

For a nice introduction to Bayesian networks, check out this blog post [https://www.probabilisticworld.com/bayesian-belief-networks-part-1/](https://www.probabilisticworld.com/bayesian-belief-networks-part-1/)

## Introduction

Bayesian networks are a compact graphical representation of the probabilistic relationship between variables. Bayesian networks can be visualized as a directed graph where each node is a probability density function for a random variable. Each arrow of the network represents a conditional dependency of the probability of the variable at the head of the arrow on the value of the variable at the tail of the arrow.

In this tutorial, we will use the [OpenAI Gym simulation](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/ai-simulator-framework/simulators/openai-gym) environment [Taxi-v3](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/ai-simulator-framework/simulators/openai-gym/taxi-v3-environment) to train a Bayesian network model and use it to answer stochastic problem questions.

![Taxi Agent](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LYmLcKZqkPDaczox0i1%2F-LvA4tIQf0sbY5ijjAM4%2F-LvA6FA2bcTJ6q0Ug7th%2Ftaxi.png?alt=media&token=5be76a7f-3615-4690-9919-cd5fd4e5049f)

Bayesian networks are an artificial intelligence tool that are used visualize the conditional probabilities between observables of a system. As a taxicab driver in Gridland, our world has three observables: `LOCATION`, `HAS_PASSENGER`, and `ACTION`.

The `HAS_PASSENGER` observable can take on two values, `HAS_PASSENGER=T` and `HAS_PASSENGER=F` which denote whether there is a passenger \(presumably the correct one\) in the cab.

When we observe the taxi's `LOCATION` it can have three possible values: `AT_PICKUP_LOCATION`, `AT_DROPOFF_LOCATION`, `AT_OTHER_LOCATION`

The `ACTION` observable represents an action that the cabby took, and can be one of the following: `MOVE_TO_PICKUP`, `MOVE_TO_DROPOFF`, `DROPOFF_PASSENGER` and `PICKUP_PASSENGER`.

We will model each of these observables as a discrete probability distribution with the initial Bayesian network structure below.

![Bayesian Network For Taxi v-3](../../../.gitbook/assets/taxi-bayes-network.png)

This means that the observed `LOCATIONS` are conditional upon the values of `HAS_PASSENGER`, and the observed `ACTION`are conditional upon both the other observables.     
  
At each step of the simulation, we will be provided with a single observation for the `LOCATION` and `HAS_PASSENGER` variables and predict the conditional probability distribution for `ACTION`.   We will then use that conditional probability distribution to generate a random action for the agent to take.

## Setup

You will need several things for this tutorial:

### Install the AI Simulator Framework

* Please take a few minutes to familiarize yourself with the purpose and operation of the [Maana Q AI Simulator framework](../../../product-guide/reference-guide/ai-simulator-framework/).
* Follow the installation instructions and confirm that you can login to the Q instance.

### Clone the Bayes Agent Workspace

* Login to Q and find and clone the "**Bayes Taxi-v3 Agent**" workspace.
* Rename it to "&lt;your name&gt; Bayes Taxi-v3 Agent".

### Test your Agent

* Copy the workspace's **service id** from the Workspace -&gt; Context Panel -&gt; Info.
* Paste it into the **Agent URI** field of Simulator -&gt; OpenAI Gym -&gt; Control panel.
* Press the "Run" button and confirm the successful operation.

## Services

### External: maana-ai-bayes-net

A standard Maana Q service for performing inference \(predictions\) over Bayesian networks.   This is a generic service that could be used for multiple stochastic modeling applications, and across any domain.    This service exposes the following core schema:

![Partial Schema for maana-ai-bayes-net](../../../.gitbook/assets/screen-shot-2019-12-06-at-2.59.56-pm.png)

Where the user must provide a network in the form of a serialized JSON object with the following lexical structure:

```text
network := { nodes }
nodes := node | node "," nodes
node := observablename ": {" idspec "," statespec "," parentspec "," cptspec "}"
idspec := "id :" identifier
statespec := "[" possiblevalue "]"
parentspec := "parents: [" parentidentifier* "]"
cpt := "cpt : [" cptrows "]"
cptrows := cptrow | cptrow "," cptrows
cptrow := [ whenspec, "," ]  thenspec
whenspec := "when : {" whenvalue* "}"
thenspec := "then : {" thenvalues "}"
whenvalue := parentidentifier ":" possiblevalue
thenvalues := thenvalue | thenvalue "," thenvalues
thenvalue := possiblevalue ":" float  
```

The CombinationInput type is used to represent both a conditional/constraint \(givens\) and unknown values for which the probabilities should be predicted.    Future versions of the maana-ai-bayes-net service will feature improvements for constructing, inspecting and inferring values from Bayes network structures.

### Workspace: GOAP Taxi-v3 Agent

A Maana service which utilizes Goal-Oriented Action Planning to simulate the behavior of a taxi in the  [Taxi-v3](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/ai-simulator-framework/simulators/openai-gym/taxi-v3-environment) environment.   We will be using this service to produce evidence vectors in the learning portion of our tutorial.

### Workspace: Bayes Taxi-v3 Agent

The Bayes Taxi-v3 Agent is a template for creating your own Bayesian network agent for the  [Taxi-v3](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/ai-simulator-framework/simulators/openai-gym/taxi-v3-environment) environment.   As with any Gym agent, the top-level KnowledgeGraph has has the familiar agent protocol.

![Top Level Knowledge Graph for the Bayes Taxi Agent](../../../.gitbook/assets/screen-shot-2019-12-06-at-3.53.42-pm.png)

#### onReset

At the beginning of a simulation run, the simulator host will ask the simulator to reset itself for a new simulation.  In turn, the simulator will ask its agent\(s\) to prepare themselves for a new simulation, including some configuration information:

* `modelId`: the ID of the model \(if any\) to create/use
* `isTraining`: indicates whether the simulation is training or performance

This function is expected to return optional state it wishes to be returned to it during the simulation run, i.e., `context`.   For the Bayes Taxi Agent, we return a serialized `Model`, which includes the number of steps taken, and the serialized Bayesian network.   The function `makeModel` can be used to create a new instance of a model kind.  The `deserializeModel` and `serializeModel` functions provide type safe methods for parsing and string encoding model instances.

![The Knowledge Graph For Bayes Taxi Models](../../../.gitbook/assets/screen-shot-2019-12-06-at-4.04.11-pm.png)

#### onStep

This function is the brains of our agent.   It takes the current observations of 

* `state`: corresponds to one of the 500 possible states in the [Taxi-v3](https://maana.gitbook.io/q/v/3.2.1/product-guide/reference-guide/ai-simulator-framework/simulators/openai-gym/taxi-v3-environment) environment,
* `context`: our bayesian network

and returns a random `Action` that the simulator should perform.   The `decide` function contains makes this decision by calling the `maana-ai-bayes-net` service with the current observation and then choosing at random from the returned conditional probability distribution.     
  
The `onStep` function also implements online learning based on Bayesian updates.   At each step, it observes the behavior of an exemplar.   Ideally this would be one or more human taxi cab drivers.   For this tutorial we utilize the GOAP taxi-v3 service to provide exemplary behavior.    The logic for performing the parameter updates is contained in the `learn` function.  
  
Upon completion, the `onStep` function also returns the posterior Bayesian network, which reflects the learnings from the current step.    The `lastReward` and `lastAction` inputs are not used this agent.

![The Function Graph for the onStep Method](../../../.gitbook/assets/screen-shot-2019-12-06-at-4.21.37-pm.png)

#### onDone



### Initial Network

The structure of our taxicab network might initially look something like this. This says that `Location`, `hasPassenger` and `Action` are all discrete distributions, and that we believe _a priori_ that probabilities location and action may be conditional upon the value fo `hasPassenger`.

![](../../../.gitbook/assets/screen-shot-2019-12-03-at-7.17.59-am.png)

## Learning

Updates of Bayesian networks is an online learning rather than batch training/update method. The agent has prior distributions for the conditional probabilities of states and actions and can learn incrementally as it observes actual behavior of the simulation \(i.e., consequences of taking actions in various states\).

Imagine at each time step you are presented with a new collection of observations for what the correct action to be taken is. This knowledge can be used to incrementally adapt the network structure or of the conditional probabilities \(via MLE or Bayesian arithmetic\), \([https://arxiv.org/pdf/1302.1538.pdf](https://arxiv.org/pdf/1302.1538.pdf)\). This is referred to as _structural learning_ vs _parameter learning_, respectively, and will be discussed below.

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

What we are interested in is an update rule that we can apply to the network as our agents explores the state-action space. There is good research and information on this problem in "[Update rules for parameter estimation in Bayesian networks](https://arxiv.org/pdf/1302.1519.pdf)" and "[Parameter Estimation in Bayesian Networks](https://courses.cs.ut.ee/2009/bayesian-networks/orasmaa-liin-chapter-6.pdf)." The general update rule for the parameters is:

![The general update rule for the parameters of a Bayesian network](../../../.gitbook/assets/screen-shot-2019-12-03-at-9.52.28-am.png)

However due the specifics of our problem, each new evidence vector provides us with an observation of all variables \( e.g. the state and the action taken\). The update rule in this case becomes very simple, with equation 5 reducing to:

$$
P\hat(pa^j_i) = 1\ if\ yT\ provides\ evidence\ of\ the\ parents\ pa_i^j\ otherwise\ 0.
$$

and the top line for equation 4 becomes:

$$
theta^T = theta^{T-1} + eta * (  (1\ if\ yT\ provides\ evidence\ of\ z\ otherwise\ 0) - theta^{T-1})
$$

These equations are simple enough to implement in a lambda.

The learning rate, eta, needs to be kept sufficiently small to ensure convergence, and will diverge when it is greater than 1.

