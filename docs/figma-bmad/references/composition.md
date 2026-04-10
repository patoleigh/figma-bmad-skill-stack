# Composition Workflow

## Core sequence

Use this order when composing a screen or scoped UI area:

1. confirm scope
2. confirm purpose or primary action
3. inspect nearest existing patterns
4. define structure
5. assign components by role
6. check states
7. check spacing and layout consistency
8. decide reuse, extension, or escalation

## Working rule

- Compose from the current file outward, not from abstract preference inward.
- Reuse the strongest existing pattern first.
- Solve hierarchy before decoration.

## Anti-patterns

- Starting from a blank visual idea when the file already has patterns
- Picking components because they look similar instead of behaving correctly
- Finishing the default view while ignoring states
