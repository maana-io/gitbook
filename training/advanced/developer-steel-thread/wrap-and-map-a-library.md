# Wrap-and-Map a Library

In this lesson, you will take an [open source implementation](https://github.com/flags/GOAPy) of an AI planning algorithm, Goal-Oriented Action Planning \(GOAP\), and learn the process of _wrap-and-map._  The purpose of wrapping and mapping digital resources is to surface them to the rest of the **Digital Knowledge Layer**, making them easy to integrate into solutions in ways you control \(i.e., what is exposed and how\).

**Wrapping** a library, service, or data source is the _act_ of creating a Knowledge microservice interface \(GraphQL or REST\) that acts as a **proxy** to the resource from the microservice ecosystem.  This is the _operational_ aspect of the job and deals more with the resource side than the ecosystem side and involves managing **state**, **concurrency**, **access control**, **scale**, and **monitoring**.

**Mapping** a library, service, or data source is the _art_ of designing the **ontology** \(i.e., Kinds and functions\) for your Knowledge microservice.

{% hint style="info" %}
A **Knowledge** microservice is not just an API - it represents a micro-domain within a distributed network of **interconnected** **domains**
{% endhint %}

The goal of mapping is to harmonize one service against the broader landscape, making it maximally compatible and usable.  Some of the topics involved include **design**, **aesthetics**, **conceptualization**, **abstraction**, **factoring**, **naming**, **compatibility**, and **reusability**.

### GOAP

For this exercise, we are going to wrap-and-map an open source AI planning algorithm, Goal-Oriented Action Planning \(GOAP\).  For a nice explanation and example, see the blog post "[Goal Oriented Action Planning for a Smarter AI](https://gamedevelopment.tutsplus.com/tutorials/goal-oriented-action-planning-for-a-smarter-ai--cms-20793)."

We will use a simple example \(from the source\) throughout this lesson.

The basic idea is to model a planning problem as:

* a set of boolean _world_ states, e.g.
  * `hungry`, `has_food`, `in_kitchen`, `tired`, `in_bed`
* a set of actions that can be taken and what _preconditions_ must exist and what the _postconditions_ will be, both in terms of world state, e.g.,
  * eat
    * Pre: `hungry=T`, `has_food=F`, `in_kitchen=F`
    * Post: `hungry=F`
* actions can also have costs
* and a goal, also specified in terms of world state, e.g.,
  * `hungry=F`

The planning algorithm then attempts to find the sequence of actions to take, minimizing costs, that transforms the current world state into the goal world state. 

Let's wrap and map this service and make it available as a building-block for our solutions.

### Prerequisites

* Completion of [Create a Microservice using the CLI](create-a-microservice-using-the-cli.md)
* **Dependencies**:
  * VS Code
  * Maana CLI
  * Python 3.7 \(+PIP\)
  * Docker

## Step-by-Step Instructions

**Step 1.** Include the target resource into our project

We are wrapping and mapping an open source Python library called GOAPy, as is customary in the Python world to call your library something ending in "-py".  In this case, it is single-file Python implementation of the Goal-Oriented Action Planning algorithm.

**Step 1a.** Visit the GitHub repository

The library is hosted publicly on GitHub: [https://github.com/flags/GOAPy](https://github.com/flags/GOAPy).

**Step 1b.** Visit the main file `goapy.py`

Since this is a single-file Python implementation, we can easily incorporate it into our service by copying the file: [https://github.com/flags/GOAPy/blob/master/goapy.py](https://github.com/flags/GOAPy/blob/master/goapy.py).

![](../../../.gitbook/assets/image%20%2882%29.png)

**Step 1c.** View the raw contents

Click the **RAW** button to gain access to the raw file contents.

![](../../../.gitbook/assets/image%20%2899%29.png)

**Step 1d.** Select all of the content and copy it to the clipboard

**Step 1e.** Create a `goapy.py` file in your VS Code project

Create the file in the app folder next to `main.py`.  Paste the raw file contents from GitHub.  Save the file.

![](../../../.gitbook/assets/image%20%28117%29.png)

**Step 2.** Create a GraphQL Knowledge model for the service



![](../../../.gitbook/assets/image%20%2881%29.png)



