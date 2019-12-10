---
description: >-
  Use classic Q learning on a small reasoning task using the Maana Q AI
  Simulator framework.
---

# Reinforcement Learning: Q-Learning

Reinforcement learning involves an [agent](https://en.wikipedia.org/wiki/Intelligent_agent), a set of states {\displaystyle S}![S](https://wikimedia.org/api/rest_v1/media/math/render/svg/4611d85173cd3b508e67077d4a1252c9c05abca2), and a set {\displaystyle A}![A](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) of actions per state. By performing an action {\displaystyle a\in A}![a\in A](https://wikimedia.org/api/rest_v1/media/math/render/svg/a97387981adb5d65f74518e20b6785a284d7abd5), the agent transitions from state to state. Executing an action in a specific state provides the agent with a reward \(a numerical score\).

The goal of the agent is to maximize its total \(future\) reward. It does this by adding the maximum reward attainable from future states to the reward for achieving its current state, effectively influencing the current action by the potential future reward. This potential reward is a weighted sum of the [expected values](https://en.wikipedia.org/wiki/Expected_value) of the rewards of all future steps starting from the current state.

The goal of Q-learning is to learn a policy, which tells an agent what action to take under what circumstances. It does not require a model of the environment \(hence the connotation "model-free"\), and it can handle problems with stochastic transitions and rewards, without requiring adaptations.

![](../../../.gitbook/assets/image%20%28147%29.png)

This example is based on this [blog post](https://tiewkh.github.io/blog/qlearning-openaitaxi/).

## Agent Protocol, Context, and Algorithm Hyperparameters

For Q-learning, in addition to the standard agent protocol, we introduce two new Kinds:

* `Hyperparameters` define the set of algorithm tuning parameters that affect how it performs
  * learning rate \(alpha\) determines to what extent newly acquired information overrides old information
  * discount factor \(gamma\) determines the importance of future rewards
  * exploitation vs exploration \(epsilon\)
* `Model` represents our state that is serialized/deserialized between invocations by the simulator

![](../../../.gitbook/assets/image%20%28163%29.png)

## onReset



![](../../../.gitbook/assets/image%20%2835%29.png)

## makeModel

![](../../../.gitbook/assets/image%20%28171%29.png)

```javascript
const { hyperparameters } = input

const id = input.id || new Date()
const actionSpace = input.actionSpace || 6
const stateSpace = input.stateSpace || 500
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

return model
```

## onStep

![](../../../.gitbook/assets/image%20%28133%29.png)

## learn

```javascript
const { newState, lastReward, lastAction, step, model, hyperparameters } = input
const { gamma, learning_rate } = hyperparameters
const { lastState } = model

// Table helper functions
const offset = (state, action) => state * model.actionSpace + action
const tableGet = (state, action) => model.table[offset(state, action)]
const tableSet = (state, action, val) => model.table[offset(state, action)] = val

// Select the max action value for a given state
const maxAction = state => {
  const start = state * model.actionSpace
  const end = start + model.actionSpace 
  return Math.max(...model.table.slice(start, end))
}

// Get the current Q table value for the previous state / action pair
const curVal = tableGet(lastState[0], lastAction[0])

// Calculate new value using Bellman's equation
const newVal = curVal + learning_rate * (lastReward[0] + gamma * maxAction(newState[0]) - curVal)

// Update the Q table
tableSet(lastState[0], lastAction[0], newVal)

// Update the model (i.e., our state)
model.steps += 1 
model.lastState = newState

return model
```

## decide

```javascript
const { state, model, hyperparameters } = input
const { min_epsilon, max_epsilon, steps_per_episode, decay_rate, gamma } = hyperparameters

// Index of max value of an array of numbers
const argMax = a => a.reduce((iMax, x, i, arr) => x > arr[iMax] ? i : iMax, 0);

// Index of action for a state with the largest Q-value
const argMaxAction = state => {
  const start = state * model.actionSpace
  const end = start + model.actionSpace 
  return argMax(model.table.slice(start, end))
}

// --- Explore vs exploit tradeoff

// adjust the rate at which we explore vs exploit
const episode = (model.steps % steps_per_episode) === 0
const epsilon = min_epsilon + (max_epsilon - min_epsilon) * Math.exp(-decay_rate*episode)

let action
if (Math.random() > epsilon) {
  action = argMaxAction(state[0]) // exploit
} else {
  action = Math.floor(Math.random() * model.actionSpace) // explore
}

return {
  id: new Date(),
  action: [action],
  context: JSON.stringify(model)
}
```

