# Components and Variants

## Reuse-first rule

- Reuse an existing component if it already covers the purpose and main behavior.
- Extend a component when the pattern is already correct but coverage is incomplete.
- Create a new component only when the current library cannot represent the needed role cleanly.

## Minimum specification for a component

Use this checklist when deciding whether a component is system-ready:

- purpose
- anatomy
- expected states
- expected variants
- basic accessibility implications

This comes directly from the BMAD component-strategy material.

## States

- Do not review only the default state.
- At minimum, inspect whether the pattern needs states such as default, hover, active, disabled, error, loading, success, or empty.
- If a state is required by the pattern but missing from the system, treat that as a real gap.

## Variants

- Keep variants explicit and predictable.
- Only add a variant when it represents a repeated and reusable difference.
- Do not multiply variants for one-off visual exceptions.

## Pattern categories to watch

BMAD material highlights these as recurring system patterns:

- buttons
- forms
- navigation
- feedback
- loading
- empty states
- search and filtering

If the current task touches one of these, check whether the system already defines it consistently.

## Gap analysis

Ask these questions before creating anything new:

- Does the library already contain the base pattern?
- Is the issue missing coverage or missing purpose?
- Can the need be solved by adding a state or variant?
- Would a new component duplicate an existing pattern?

## Anti-patterns

- Creating a new component because the old one needs cleanup
- Duplicating a component family to solve a single page problem
- Encoding content-specific behavior into a supposedly reusable component
- Ignoring states and calling the component complete
