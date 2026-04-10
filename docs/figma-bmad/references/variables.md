# Variables and Tokens

## Core rules

- Prefer existing semantic variables or styles before introducing new values.
- If a value repeats and carries a system role, normalize it instead of leaving it local.
- Keep the system lean. Create the smallest useful set of variables that supports consistency.
- Use variables to support consistency across components, not to create abstract complexity.

## Color

- Map color by semantic role where the role is known.
- Keep contrast in mind when defining or reusing semantic colors.
- Avoid duplicating nearly identical colors under different names without a real role difference.

## Typography

- Reuse an existing text scale if one exists.
- If text styles are inconsistent, normalize the most reused roles first.
- Do not create page-specific text styles when a reusable role already exists.

## Spacing

- Treat spacing as a system rhythm, not as isolated manual tweaks.
- Prefer a small repeatable spacing pattern over many one-off values.
- If repeated layouts depend on spacing, stabilize the spacing before creating more components.

## Figma translation note

- BMAD source material talks about spacing, grid, and layout foundation.
- Translating that into Figma, use variables and consistent auto layout spacing where repeated structures exist. This is an inference, but it is a direct one.

## Creation rules

- Reuse before adding.
- Extend an existing semantic set before creating parallel naming.
- If a variable cannot be named semantically yet, flag it as unresolved instead of pretending the role is clear.

## Anti-patterns

- Hardcoded local values repeated across many components
- Creating several tokens for the same role
- Naming tokens only by raw value when the semantic role is known
- Letting overrides become the real system
