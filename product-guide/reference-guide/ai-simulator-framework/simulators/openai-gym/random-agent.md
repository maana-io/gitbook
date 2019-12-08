---
description: Generates a random action sampled from the action space
---

# Random Agent

Find the "Random AI Agent" workspace and clone it.  On LKG, the link is: [https://lastknowngood.knowledge.maana.io/workspace/46661294-c682-4cbd-8e05-78e1db2a1229](https://lastknowngood.knowledge.maana.io/workspace/46661294-c682-4cbd-8e05-78e1db2a1229).

The simplest action an Agent can take is to randomly select an action from the action space.

In `onReset`, create context by populating the `Model` Kind instance with the `actionSpace` argument.

In `onStep`, use the information about the action space from the serialized `Model` Kind to generate a random action.

Simply return `true` in `onDone` to indicate success.



