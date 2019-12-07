# Wrap-and-Map a Library

In this lesson, you will take an [open source implementation](https://github.com/flags/GOAPy) of an AI planning algorithm, Goal-Oriented Action Planning \(GOAP\), and learn the process of _wrap-and-map._  The purpose of wrapping and mapping digital resources is to surface them to the rest of the **Digital Knowledge Layer**, making them easy to integrate into solutions in ways you control \(i.e., what is exposed and how\).

**Wrapping** a library, service, or data source is the _act_ of creating a Knowledge microservice interface \(GraphQL or REST\) that acts as a **proxy** to the resource from the microservice ecosystem.  This is the _operational_ aspect of the job and deals more with the resource side than the ecosystem side and involves managing **state**, **concurrency**, **access control**, **scale**, and **monitoring**.

**Mapping** a library, service, or data source is the _art_ of designing the **ontology** \(i.e., Kinds and functions\) for your Knowledge microservice.

{% hint style="info" %}
A **Knowledge** microservice is not just an API - it represents a micro-domain within a distributed network of **interconnected** **domains**
{% endhint %}

The goal of mapping is to harmonize one service against the broader landscape, making it maximally compatible and usable.  Some of the topics involved include **design**, **aesthetics**, **conceptualization**, **abstraction**, **factoring**, **naming**, **compatibility**, and **reusability**.

### Prerequisites

* Completion of [Create a Microservice using the CLI](create-a-microservice-using-the-cli.md)
* **Dependencies**:
  * VS Code
  * Maana CLI
  * Python 3.7 \(+PIP\)
  * Docker

## Step-by-Step Instructions

**Step 1.** Create your project scaffolding

