# State Prioritization

Use this reference during `figma-bmad-prd-to-screen-plan` to identify which critical states composition must address for each view.

## Purpose of state identification at planning stage

At the planning stage, the goal is not to enumerate every possible state. The goal is to flag the states that would be visibly missing at composition time if not planned for. Composition cannot complete a view safely if key states were not anticipated in the plan.

This reference is different from `references/state-coverage.md`, which is used during handoff readiness to judge whether composed states are sufficient. This reference guides which states to flag *before* composition begins.

## States to flag at planning stage

For each view, consider whether these states are critical to its correct operation:

### Default
Almost always required. The view as it appears when data is available and no action is in progress.

### Loading
Required when the view retrieves data asynchronously. Flag if the view depends on a backend call, a slow operation, or a deferred data source.

### Empty
Required when the view shows a list, collection, or data set that may have zero items. An empty state is a distinct composition challenge — flag it if the view involves any collection.

### Error
Required when the view involves a form submission, an action that can fail, or a data fetch that may return an error. Flag if the requirements mention success/failure or validation.

### Success or confirmation
Required when the primary action has a visible outcome — form submitted, item created, action completed. May be a distinct state, an overlay, or a brief feedback moment.

### Disabled or locked
Required when the view or its primary action may be unavailable based on user role, permissions, or system state. Flag if requirements mention conditions for availability.

### Partial or in-progress
Required when the primary action is multi-step or can be interrupted. Flag if requirements describe a flow with intermediate states.

## How to decide which states to flag

Flag a state as critical for a view when:

- the requirements explicitly mention it
- the primary action of the view would be ambiguous without it
- the view involves a user flow that has a known success/failure path
- composition would leave a visible gap if that state were missing

Do not flag a state as critical when:

- it is clearly not applicable to the view's purpose
- the requirements provide no evidence that the state is needed
- it is a micro-interaction or edge case that falls below the planning threshold

## Working rule

If in doubt, flag the state. It is better to surface a state for composition to resolve than to leave it unplanned and have it become a handoff readiness blocker.

## Anti-patterns

- Treating the default state as the only state that matters
- Omitting the empty state for any view that involves a list or collection
- Assuming error states are handled globally without flagging them at the view level
- Over-flagging every conceivable state at the planning level — stay focused on states that are critical to the view's primary interaction
