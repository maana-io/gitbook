---
description: Beyond Lambdas
---

# Knowledge Microservices

## Overview

In our lessons thus far, anytime we've needed to write some custom code, we've used a JavaScript lambda function.  These are fine for what they are intended: short, relatively simple, self-contained \(i.e., minimal external dependencies\) code blocks.  However, there are many cases where full-blown containerized microservices, written in Python, Scala, C\#, Go, Rust, C++, NodeJS, TensorFlow, Spark, etc. are needed to be deployed at scale.

## Introduction

A Maana Q solution follows a **top-down methodology**: what is the problem we're solving?  We frame the problem in terms of a question of the form: Given X, what is Y?  This is called the top-level **problem question** \(PQ\).

Problem _decomposition_ follows by generating more, lower-level PQs.  As **developers**, we know that PQs are really just **functions** in disguise.

Therefore, the process of **problem decomposition** is _really_ one of **function composition**.  One _deconstructs_ or _breaks-down_ the problem, the other _constructs_ or _builds-up_ the solution.

Each of the functions being composed on a CKG **function graph** can either themselves be function compositions \(i.e., nesting function graphs\) or **external** **microservices** \(GraphQL\).  These become **black boxes** to the rest of the solution, as we only know them by what they expose via their interface **schema**.  In other words, we know _what_ they do, but not _how_ they do it.

Microservices allow big \(monolithic\) domains to broken down into smaller domains and solved incrementally, providing reusable building blocks.  Who doesn't love playing with blocks?

{% hint style="success" %}
Make fun building blocks for people to play with
{% endhint %}

## Lesson Goals

* Using the Maana CLI to create new Q-ready microservices
* Wrap-and-map a service
* Test a service locally
* Deploy a Dockerized service to Kubernetes
* Register a service with Q

