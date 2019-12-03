---
description: >-
  Use Goal-Oriented Action Planning (GOAP) to solve a reasoning task using the Q
  AI Simulator framework.
---

# Logical Inference and AI Planning with GOAP

[Goal-Oriented Action Planning \(GOAP\)](http://alumni.media.mit.edu/~jorkin/goap.html) is a simple, but popular AI planner that uses logical chaining to achieve goals by performing a sequence of actions that change the world state \(from preconditions to postconditions\).  States are generally boolean conditions and actions can have associated costs and the planner will find the cheapest sequence.

## Setup

For this exercise, we are going to use the [Maana Q AI Simulator framework](../../../product-guide/reference-guide/ai-simulator-framework/).  Please take a few minutes to familiarize yourself with its purpose and operation.  Clone the "Random Taxi-v3 Agent" workspace and configure your OpenAI Gym simulator for the Taxi-v3 environment using your cloned agent's service URI.  \(Leave the token field blank.\)

## maana-ai-goap

## Functions

### taxiStateToGOAPScenario

```javascript
  const { taxiState } = input
  const { isAtPickupLocation, isAtDropoffLocation, isWithPassenger } = taxiState
  
  return {
    id: 'taxi-v3',
    goal: [
      {
        id: 'IS_DONE',
        val: true
      }
    ],
    state: [
      {
        id: 'AT_PICKUP_LOCATION',
        val: isAtPickupLocation
      },
      {
        id: 'AT_DROPOFF_LOCATION',
        val: isAtDropoffLocation
      },
      {
        id: 'WITH_PASSENGER',
        val: isWithPassenger
      },
      {
        id: 'IS_DONE',
        val: false
      }
    ],
    actions: [
      {
        id: 'MOVE_TO_PICKUP_LOCATION',
        pre: [
          {
            id: 'AT_PICKUP_LOCATION',
            val: false
          },
          {
            id: 'WITH_PASSENGER',
            val: false
          }
        ],
        post: [
          {
            id: 'AT_PICKUP_LOCATION',
            val: true
          }
        ]
      },
      {
        id: 'PICKUP',
        pre: [
          {
            id: 'AT_PICKUP_LOCATION',
            val: true
          },
          {
            id: 'WITH_PASSENGER',
            val: false
          }
        ],
        post: [
          {
            id: 'AT_PICKUP_LOCATION',
            val: false
          },
          {
            id: 'WITH_PASSENGER',
            val: true
          }
        ]
      },
      {
        id: 'MOVE_TO_DROPOFF_LOCATION',
        pre: [
          {
            id: 'AT_DROPOFF_LOCATION',
            val: false
          },
          {
            id: 'WITH_PASSENGER',
            val: true
          }
        ],
        post: [
          {
            id: 'AT_DROPOFF_LOCATION',
            val: true
          }
        ]
      },
      {
        id: 'DROPOFF',
        pre: [
          {
            id: 'AT_DROPOFF_LOCATION',
            val: true
          },
          {
            id: 'WITH_PASSENGER',
            val: true
          }
        ],
        post: [
          {
            id: 'IS_DONE',
            val: true
          }
        ]
      }
    ]
  }



```

