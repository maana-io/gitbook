---
description: Build your first Maana Q service
---

# Hello, world!

## Overview

In this hands-on tutorial, you will learn the fundamental operations and user interface elements of building Maana Q solutions.  We introduce Q with the traditional "Hello, world!" example and build some interesting capabilities quickly.

## Introduction

The core of Maana Q is the [**Computational Knowledge Graph \(CKG\)**](../../../product-guide/platform-features/computational-knowledge-graph/), which consists of the combination of general and specialized **reasoners** \(calculations, transformations, inferences, predictions, simulations, etc.\) and **graphs** \(i.e., nodes and edges\) that represent a _domain_ over which we wish to reason.

{% hint style="success" %}
The purpose of reasoning is to achieve desired goals
{% endhint %}

The form of reasoning in Q, unlike [other knowledge systems](https://en.wikipedia.org/wiki/Semantic_Web), is completely general.  Q solutions are not limited to [_description logic_](https://en.wikipedia.org/wiki/Description_logic), but can use any computational technique, library, or service by exposing it via a **microservice** interface.  For Q, we use GraphQL and REST \(via OpenAPI\), with more protocol support \(e.g., gRPC\) coming soon.  This allows the right and best technology to be used for representing the domain and solving its various problems.  We refer to this with the motto:

{% hint style="success" %}
Use the right tool for the job
{% endhint %}

The system, then, consists of a federation of coordinated microservices participating in a large-scale network around a shared _ontology_.  Each _service_ \(for short\) provides a set of **concepts**, **properties**, **relations**, **instances**, and **functions** that operate on them.  Together, they represent _knowledge_ about some _domain_.  Functions provide the mechanism for interrogating the domain, i.e., asking it questions, such as "given a well plan, how long will it take it?  what is the best rig/crew to use?  expected production rates?".

{% hint style="success" %}
Knowledge is the answer to a question
{% endhint %}



