# Symbolic Logic Cheat Sheet

## State

Think: *what facts are true right now?*

- Usually stored as a collection of positive facts, and sometimes negative facts too
- Example: cargo at an airport, plane at an airport, cargo inside a plane

## Action

Think: *one legal move in the world.*

- Each action changes the state
- In this project: loading, unloading, or flying

## Preconditions

Facts that must already be true before an action can happen.

- Example: to load cargo into a plane, the cargo and plane must be at the same airport

## Effects

What the action changes. Usually split into:

- facts to **add**
- facts to **remove**

Example: after loading, “cargo in plane” becomes true, and “cargo at airport” is no longer true.

## Goal test

Ask: *does this state satisfy all required goal facts?*

- Usually means checking whether every goal proposition is present in the current state

## Applicable action

An action is applicable only if its preconditions match the current state.

- If even one required fact is missing, that action can’t be used

## Successor state

1. Start from the current state
2. Remove the action’s negative effects
3. Add the action’s positive effects

That gives the next state.

## Search view

Planning is search over states:

| | |
|---|---|
| **Nodes** | states |
| **Edges** | actions |
| **Solution** | sequence of actions reaching a goal state |

## Tracing one action

The most useful habit for this project is to trace one action manually:

1. What facts must be true first?
2. Which facts disappear?
3. Which facts appear?
4. Does the result move you closer to the goal?

> **Common bug:** mixing up preconditions with effects, or forgetting to remove an old fact when a new one replaces it.
