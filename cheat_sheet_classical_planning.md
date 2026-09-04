# Classical Planning Cheat Sheet

Forward-planning project notes.

## Classical planning

Find a sequence of actions that transforms the initial state into a goal state.

Assumes the world is:

- deterministic
- fully observable
- discrete

## Initial state

- The facts true at the start
- This is your search starting point

## Goal state

- Usually not one exact full state, but a set of facts that must be true
- A state passes the goal test if it contains all goal facts

## State-space search

- You search through possible world states
- Each step applies one valid action to produce a new state

## Action schema

A general action template, like `load`, `unload`, `fly`.

Once filled in with specific objects, it becomes a concrete action.

## Concrete action

A fully specified action instance.

- Example: load one specific cargo into one specific plane at one specific airport

## Preconditions

Conditions that must hold before an action is allowed.

- If they don’t hold, that action is not available from that state

## Effects

The state changes caused by the action:

- **Positive effects** add facts
- **Negative effects** remove facts

## Transition model

The rule for going from one state to the next by applying an action.

In this project, this is the heart of forward planning.

## Successor function

Given a state, return the actions that can be applied and/or the resulting next states.

This is what the search algorithm depends on.

## Goal test

Check whether all required goal facts are true in the current state.

- Not “close enough” — all required facts must hold

## Plan

The final answer: an ordered list of actions from start to goal.

## Search cost

- Often each action has cost 1, so shorter plans are preferred
- Search algorithms use this to compare paths

## Heuristic

An estimate of how far a state is from the goal.

- Helps search focus on promising states
- For this project, heuristics matter because uninformed search gets expensive fast

## Forward planning

Start at the initial state and apply actions forward until reaching the goal.

This is different from reasoning backward from the goal.

## Classical planning assumptions

- Actions have known outcomes
- No randomness
- No hidden information
- The world changes only through modeled actions

## Mental model

For this project:

1. Represent the current world as facts
2. Generate legal actions from that world
3. Apply one action to create a new world
4. Repeat until the goal facts are all true

> **Self-check:** If I apply this action, can I clearly say which facts stay, which facts are added, and which facts are removed? If yes, you’re thinking about the project the right way.
