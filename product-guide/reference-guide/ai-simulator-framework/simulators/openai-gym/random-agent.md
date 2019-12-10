---
description: Generates a random action sampled from the action space
---

# Random Agent

The simplest action an agent can take is to randomly select an action from the action space.

## onReset

In `onReset`, we create our _context_ \(state, model\) by populating a `Model` Kind instance with the `actionSpace` argument.  We prefer to work with strongly-typed data \(instances\).  The protocol between the simulator does not allow us to return an arbitrary type.  Our solution is to work internally with a strong type, Model, and serialize/deserialize to/from a common `STRING` for maintaining our state between simulator invocations.

This is implemented in a simple lambda function:

```javascript
// Use the actionSpace as our context
return input.actionSpace.toString()
```

## onStep

In `onStep`, we use the information about the action space from the serialized `Model` Kind to generate a random action.  Again, this is a simple lambda function:

```javascript
// Extract the actionSpace from the context (established in onReset)
const { context } = input

// Use the actionSpace to pick a random number from
const actionSpace = context ? parseInt(context) : 0
const action = Math.floor(Math.random() * actionSpace)

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



