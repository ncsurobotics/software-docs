# The Action System

## Why actions exist

A mission is easier to reason about when it is composed from small operations instead of one enormous async function. SW9S calls those operations actions.

## Beginner mental model

An action can observe something, make a decision, move, wait, or combine other actions. It has a typed result: a detector might return an offset, while a movement action may return success or failure. A chain passes one result into the next action; a sequence runs actions in order.

## Actual implementation

In `src/missions/action.rs`, `ActionExec<T>` executes an action asynchronously and `ActionMod<Input>` modifies an action with prior output. Important combinators include:

- `ActionSequence`: do one action, then another.
- `ActionChain`: pass output forward into a modified action.
- `ActionConditional` and `ActionDataConditional`: branch.
- `RaceAction`: complete when either branch completes.
- `DualAction` and `ActionConcurrent`: await multiple actions.
- `ActionUntil` and `ActionWhile`: repeat based on a condition.

`act_nest!` builds nested action trees. `src/missions/vision.rs` adapts detectors to actions; `movement.rs` adapts their outputs to motion requests.

## Important semantics

Concurrency here is not automatically safe physical parallelism. A race drops the losing future, but a previously sent hardware command remains a real side effect. Some actions discard errors depending on their inferred output type. Treat action composition as control-flow code that must be reviewed with the same care as direct movement code.

## Debugging and modification

Draw an action's input/output chain before editing it. Check cancellation, timing, and what happens after a failed detection. Prefer adding a pure transform or a logged observation before changing the final actuator action.

## Last verified against SW9S

Source-derived from `fc780a1`.
