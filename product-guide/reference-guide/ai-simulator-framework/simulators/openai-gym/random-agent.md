---
description: Generates a random action sampled from the action space
---

# Random Agent

The simplest action an agent can take is to randomly select an action from the action space.

Find the "Random AI Agent" workspace and clone it.  On LKG, the link is: [https://lastknowngood.knowledge.maana.io/workspace/46661294-c682-4cbd-8e05-78e1db2a1229](https://lastknowngood.knowledge.maana.io/workspace/46661294-c682-4cbd-8e05-78e1db2a1229).

![](../../../../../.gitbook/assets/image%20%28115%29.png)

## onReset

In `onReset`, we create our _context_ \(state, model\) by populating a `Model` Kind instance with the `actionSpace` argument.  We prefer to work with strongly-typed data \(instances\).  The protocol between the simulator does not allow us to return an arbitrary type.  Our solution is to work internally with a strong type, Model, and serialize/deserialize to/from a common `STRING` for maintaining our state between simulator invocations.

This is implemented in a simple lambda function:

```javascript
// Construct an instance of a 'model'
const model = { 
  id: "0",
  actionSpace: input.actionSpace 
}

// Return serialized model
return JSON.stringify(model)

```

## onStep

In `onStep`, we use the information about the action space from the serialized `Model` Kind to generate a random action.  Again, this is a simple lambda function:

```javascript
const { context } = input
const { actionSpace } = JSON.parse(context || "{}")
const action = !!actionSpace 
  ? Math.floor(Math.random() * actionSpace)
  : 0
return {
  id: action,
  action: [action],
  context
}
```

## onDone

Simply return `true` in `onDone` to indicate success using a trivial lambda:

```javascript
return true
```



