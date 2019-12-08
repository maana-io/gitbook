# Wrap-and-Map a Python Library

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

A complete example is included in the GitHib repo that we will use to drive and test our implementation:

```python
from goapy import Planner, Action_List

if __name__ == '__main__':
    import time

    _world = Planner('hungry', 'has_food', 'in_kitchen', 'tired', 'in_bed')
    _world.set_start_state(hungry=True, has_food=False, in_kitchen=False, tired=True, in_bed=False)
    _world.set_goal_state(tired=False)

    _actions = Action_List()
    _actions.add_condition('eat', hungry=True, has_food=True, in_kitchen=False)
    _actions.add_reaction('eat', hungry=False)
    _actions.add_condition('cook', hungry=True, has_food=False, in_kitchen=True)
    _actions.add_reaction('cook', has_food=True)
    _actions.add_condition('sleep', tired=True, in_bed=True)
    _actions.add_reaction('sleep', tired=False)
    _actions.add_condition('go_to_bed', in_bed=False, hungry=False)
    _actions.add_reaction('go_to_bed', in_bed=True)
    _actions.add_condition('go_to_kitchen', in_kitchen=False)
    _actions.add_reaction('go_to_kitchen', in_kitchen=True)
    _actions.add_condition('leave_kitchen', in_kitchen=True)
    _actions.add_reaction('leave_kitchen', in_kitchen=False)
    _actions.add_condition('order_pizza', has_food=False, hungry=True)
    _actions.add_reaction('order_pizza', has_food=True)
    _actions.set_weight('go_to_kitchen', 20)
    _actions.set_weight('order_pizza', 1)

    _world.set_action_list(_actions)
    
    _t = time.time()
    _path = _world.calculate()
    _took_time = time.time() - _t

    for path in _path:
        print(_path.index(path)+1, path['name'])

    print('\nTook:', _took_time)
```

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

![](../../../.gitbook/assets/image%20%28119%29.png)

**Step 1f.** Add support for `numpy`

This algorithm has a dependency on the common `numpy` library, which is not included in the project template \(for size reasons\).  You will need to install it locally in order to run locally.

Stop your service and `pip install numpy`, then restart your service `./start-reload.sh`.

**Step 2.** Create a GraphQL Knowledge model for the service

As we previously described, the conceptual model involves: **states**, **actions**, and **goals**.  We can combine these into the concept of a **scenario** that we submit to the planner.  We generally wish to avoid maintaining state within low-level services, so we prefer to send everything it needs in order to function, within reason.

We can capture these abstraction with the following simple GraphQL model:

```graphql
type GoapState {
  id: ID!
  val: Boolean!
}

type GoapAction {
  id: ID!
  pre: [GoapState!]!
  post: [GoapState!]!
}

type GoapScenario {
  id: ID!
  goal: [GoapState!]!
  state: [GoapState!]!
  actions: [GoapAction!]!
}
```

Note that we've prefixed the names with `Goap` in order to avoid potential naming conflicts.  We intend for this service to be included by others, which means merging the type definitions.  There are ways of dealing with name conflicts, but it is better to use distinct names in lower-level libraries that are expected to be reused.

Note also that we've included the required identity fields for our types, since we expect them to be used directly by Maana Q.  \(This restriction will be lifted in a subsequent platform update.\)

{% hint style="info" %}
Always include an `id: ID!`field in your GraphQL types for Maana Q compatibility
{% endhint %}

The only **function** we need to expose is the main plan operation:  

> Given a planning **scenario**, what is the sequence of **actions** to take to achieve the goal?

```graphql
type Query {
  plan(scenario: GoapScenarioInput!): [ID!]!
}
```

Note that we are returning simply a list of IDs representing the sequence of **actions** to perform.  Full Action object include their pre- and post-conditions, and we only care about the action identifiers \(e.g., `eat`\).

Recall that GraphQL requires you to use input types as arguments to queries and mutations.  Therefore, we need to expand our full schema to include input types.

**Step 2a.**  Replace the existing GraphQL schema with the new design

Cut-and-paste the following complete schema into the `main.py` file, replacing the call to the `gql` function.

```graphql
type GoapState {
  id: ID!
  val: Boolean!
}

type GoapAction {
  id: ID!
  pre: [GoapState!]!
  post: [GoapState!]!
}

type GoapScenario {
  id: ID!
  goal: [GoapState!]!
  state: [GoapState!]!
  actions: [GoapAction!]!
}

input GoapStateInput {
  id: ID!
  val: Boolean!
}

input GoapActionInput {
  id: ID!
  pre: [GoapStateInput!]!
  post: [GoapStateInput!]!
}

input GoapScenarioInput {
  id: ID!
  goal: [GoapStateInput!]!
  state: [GoapStateInput!]!
  actions: [GoapActionInput!]!
}

type Query {
  plan(scenario: GoapScenarioInput!): [ID!]!
}
```

**Step 3.** Implement the resolver

Now that we have our schema \(remember: we're schema-first\), we can think about mapping it to the library.

The primary entry point is the `plan` query for which we must write the resolver.

**Step 3a.**  Replace the resolver with our new one

It is best practice to keep resolver functions minimal by having their main logic implemented by a separate function.

```python
@query.field("plan")
def resolve_plan(*_, scenario):
    return plan(scenario)


def plan(scenario):
```

**Step 3b.** Create a planning instance

Examining the example more closely, we see that the Planner object takes a set of state identifiers:

```python
_world = Planner('hungry', 'has_food', 'in_kitchen', 'tired', 'in_bed')
```

Our `Scenario` type includes a collection of `State`s, which we can extract just the identifiers from to pass to the `Planner`.

```python
keys = [x["id"] for x in scenario["state"]]
_world = Planner(*keys)
```

**Step 3c.** Define the start and goal states for the planner

Next, the example code provides the initial and goal states to the planner:

```python
_world.set_start_state(hungry=True, has_food=False, in_kitchen=False, tired=True, in_bed=False)
_world.set_goal_state(tired=False)
```

Our format is modeled as: `{"id": "hungry", "val": true}` , since we need solid structure to match our type, but the expected format is `{"hungry": true}`.  We can introduce a helper function that generically performs this conversion:

```python
def make_object(vars):
    obj = {}
    for x in vars:
        obj[x["id"]] = x["val"]
    return obj
```

Then we can use this to extract the states in the form we need them:

```python
initial_state = makeObject(scenario["state"])
_world.set_start_state(**initial_state)

goal_state = make_object(scenario["goal"])
_world.set_goal_state(**goal_state)
```

**Step 3d.** Define the actions for the planner

Each action and its pre- and post-conditions are set:

```python
_actions = Action_List()
_actions.add_condition('eat', hungry=True, has_food=True, in_kitchen=False)
_actions.add_reaction('eat', hungry=False)
# ...
_world.set_action_list(_actions)
```

We can translate this to work with arbitrary actions using our helper function:

```python
_actions = Action_List()

for action in scenario["actions"]:
    name = action["id"]
    pre = make_object(action["pre"])
    post = make_object(action["post"])
    _actions.add_condition(name, **pre)
    _actions.add_reaction(name, **post)
_world.set_action_list(_actions)
```

**Step 3e.**  Plan and return actions

Lastly, it asks the planner to solve the scenario:

```python
_path = _world.calculate()
```

We can keep this the same as the example.

The example simply displays to the console which actions it planned:

```python
for path in _path:
        print(_path.index(path)+1, path['name'])
```

We, on the other hand, need to return the collection of action ids  to our caller:

```python
plan = [p["name"] for p in _path]
return plan
```

#### Final Listing

The complete listing for `main.py`:

```python
# --- External imports
from ariadne.asgi import GraphQL
from ariadne import ObjectType, QueryType, gql, make_executable_schema
import numpy as np
import threading
import time
import json
import sys
import os
from asgi_lifespan import Lifespan, LifespanMiddleware
from app.goapy import World, Planner, Action_List

# --- GraphQL


# Map resolver functions to Query and Mutation fields
query = QueryType()

# Define types using Schema Definition Language (https://graphql.org/learn/schema/)
# Wrapping string in gql function provides validation and better error traceback
type_defs = gql("""

# Boilerplate
type Info {
  id: ID!
  name: String!
  description: String
}

type GoapState {
  id: ID!
  val: Boolean!
}

type GoapAction {
  id: ID!
  pre: [GoapState!]!
  post: [GoapState!]!
}

type GoapScenario {
  id: ID!
  goal: [GoapState!]!
  state: [GoapState!]!
  actions: [GoapAction!]!
}

input GoapStateInput {
  id: ID!
  val: Boolean!
}

input GoapActionInput {
  id: ID!
  pre: [GoapStateInput!]!
  post: [GoapStateInput!]!
}

input GoapScenarioInput {
  id: ID!
  goal: [GoapStateInput!]!
  state: [GoapStateInput!]!
  actions: [GoapActionInput!]!
}

type Query {
  info: Info!
  plan(scenario: GoapScenarioInput!): [ID!]!
}

""")


def make_object(vars):
    obj = {}
    for x in vars:
        obj[x["id"]] = x["val"]
    return obj


def plan(scenario):

    keys = [x["id"] for x in scenario["state"]]
    _world = Planner(*keys)

    initial_state = make_object(scenario["state"])
    _world.set_start_state(**initial_state)

    goal_state = make_object(scenario["goal"])
    _world.set_goal_state(**goal_state)

    _actions = Action_List()

    for action in scenario["actions"]:
        name = action["id"]
        pre = make_object(action["pre"])
        post = make_object(action["post"])
        _actions.add_condition(name, **pre)
        _actions.add_reaction(name, **post)
    _world.set_action_list(_actions)

    _t = time.time()
    _path = _world.calculate()
    _took_time = time.time() - _t

    plan = [p["name"] for p in _path]

    print('\nTook:', _took_time)

    return plan


def info():
    return {
        'id': "maana-ai-goap",
        'name': "Goal-Oriented Action Planning in Python",
        'description': ""
    }

# Resolvers are simple python functions
@query.field("info")
def resolve_info(*_):
    return info()


@query.field("plan")
def resolve_plan(*_, scenario):
    return plan(scenario)


# Create executable GraphQL schema
schema = make_executable_schema(type_defs, [query])

# --- ASGI app

# 'Lifespan' is a standalone ASGI app.
# It implements the lifespan protocol,
# and allows registering lifespan event handlers.
lifespan = Lifespan()


@lifespan.on_event("startup")
async def startup():
    print("Starting up...")
    print("... done!")


@lifespan.on_event("shutdown")
async def shutdown():
    print("Shutting down...")
    print("... done!")

# Create an ASGI app using the schema, running in debug mode
app = GraphQL(schema, debug=True)

# 'LifespanMiddleware' returns an ASGI app.
# It forwards lifespan requests to 'lifespan',
# and anything else goes to 'app'.
app = LifespanMiddleware(app, lifespan=lifespan)

```

Step 4.  Test the service

With our schema defined and our service implemented, we can try it by giving it a planning task.  Let's give it the same one as the example.

**Step 4a.** Create a `playground.gql` file in the project at the root

We have found it helpful to create a `playground.gql` file with your service that illustrates basic usage and can be used to [smoke test](https://en.wikipedia.org/wiki/Smoke_testing_%28software%29) your service for someone just getting familiar with it.

![](../../../.gitbook/assets/image%20%28139%29.png)

**Step 4b.** Create a GOAP Scenario instance for planning

Here is the start.  Copy-and-paste this into your `playground.gql` file and save it.

```graphql
query SimplePlan {
  plan(
    scenario: {
      id: 0
      goal: [{ id: "hungry", val: false }]
      state: [{ id: "hungry", val: true }]
      actions: [
        {
          id: "eat"
          pre: [{ id: "hungry", val: true }]
          post: [{ id: "hungry", val: false }]
        }
      ]
    }
  )
}
```

**Step 4c.** Issue the query in playground

Assuming your service is still running \(`./start-reload.sh`\), open the browser session with GraphQL Playground and paste your query into the IDE.

![](../../../.gitbook/assets/image%20%2881%29.png)

**Challenge:** Complete the example scenario

Can you extend the initial model above to the complete example scenario?

```graphql
    _world = Planner('hungry', 'has_food', 'in_kitchen', 'tired', 'in_bed')
    _world.set_start_state(hungry=True, has_food=False, in_kitchen=False, tired=True, in_bed=False)
    _world.set_goal_state(tired=False)

    _actions = Action_List()
    _actions.add_condition('eat', hungry=True, has_food=True, in_kitchen=False)
    _actions.add_reaction('eat', hungry=False)
    _actions.add_condition('cook', hungry=True, has_food=False, in_kitchen=True)
    _actions.add_reaction('cook', has_food=True)
    _actions.add_condition('sleep', tired=True, in_bed=True)
    _actions.add_reaction('sleep', tired=False)
    _actions.add_condition('go_to_bed', in_bed=False, hungry=False)
    _actions.add_reaction('go_to_bed', in_bed=True)
    _actions.add_condition('go_to_kitchen', in_kitchen=False)
    _actions.add_reaction('go_to_kitchen', in_kitchen=True)
    _actions.add_condition('leave_kitchen', in_kitchen=True)
    _actions.add_reaction('leave_kitchen', in_kitchen=False)
    _actions.add_condition('order_pizza', has_food=False, hungry=True)
    _actions.add_reaction('order_pizza', has_food=True)
    _actions.set_weight('go_to_kitchen', 20)
    _actions.set_weight('order_pizza', 1)
```

**Challenge:** Extend the solution to include costs

As mentioned at the beginning, the GOAP algorithm can also incorporate the costs of various actions, leading to an optimization opportunity to find the least costly plans.  Can you extend the ontology and implement the changes to support this feature?

## Conclusions

In this lesson, you:

* Ripped some open source code from GitHub
* Install Python packages locally
* Designed a mini-ontology for the domain of GOAP-based AI planning
* Implemented a GraphQL schema and resolvers in Python
* Crafted a GOAP scenario using your domain model
* Tested your Python GraphQL microservice locally using GraphQL Playground

In the next lesson, we take your service to the cloud...

