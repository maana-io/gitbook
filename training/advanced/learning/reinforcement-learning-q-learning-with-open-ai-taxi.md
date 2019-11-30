---
description: >-
  Use classic Q learning on a small reasoning task using the Maana Q AI
  Simulator framework.
---

# Reinforcement Learning: Q-Learning with Open AI Taxi

This example is based on [this blog post](https://tiewkh.github.io/blog/qlearning-openaitaxi/).

```text
const { hyperparameters } = input

const id =  input.id | new Date(),
const actionSpace = input.actionSpace | 6
const stateSpace = input.stateSpace | 500
const tableSize = actionSpace * stateSpace
const table = new Float32Array(tableSize)

const model = {
  id,
  actionSpace,
  stateSpace,
  table,
  lastState: [0],
  steps: 0,
  epsilon: hyperparameters.max_epsilon
}

return JSON.stringify(model)
```

```text
const { newState, lastReward, lastAction, isDone, context, hyperparameters } = input
const { gamma, learning_rate } = hyperparameters
const { lastState, model } = context

// Table helper functions
const offset = (state, action) = state * model.actionSpace + action
const tableGet = (state, action) = model.table[offset(state, action)]
const tableSet = (state, action, val) = model.table[offset(state, action)] = val

// Get the current Q table value for the previous state / action pair
const curVal = tableGet(lastState[0], lastAction[0])

// Select the max action value for a given state
const maxAction = state = {
  const start = state * model.actionSpace
  const end = start + model.actionSpace 
  return Math.max(model.table.slice(start, end))
}

// Calculate new value using Bellman's equation
const newVal = curVal + learning_rate + (lastReward[0] + gamma * maxAction(newState) - curVal)

// Update the Q table
tableSet(state, action, newVal)

return context
```

```text
const { state, model, hyperparameters } = input
const { epsilon } = hyperparameters

const exp_exp_tradeoff = Math.random()

const argMax = a => a.reduce((iMax, x, i, arr) => x > arr[iMax] ? i : iMax, 0);

const maxAction = state = {
  const start = state * model.actionSpace
  const end = start + model.actionSpace 
  return argMax(model.table.slice(start, end))
}

let action
if (exp_exp_tradeoff > hyperparameters.epsilon) {
  action = maxAction(state[0])
} else {
  action = Math.floor(Math.random() * model.actionSpace)
}

return {
  id: new Date(),
  action: [action],
  context: JSON.serialize({
    lastAction: [action],
    model
  })
}
```

