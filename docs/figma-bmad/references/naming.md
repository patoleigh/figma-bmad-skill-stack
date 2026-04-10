# Naming Rules

Inference note:

- These rules translate BMAD consistency and naming patterns into Figma-oriented guidance. They are not copied verbatim from a Figma-specific BMAD source.

## Core rules

- Name assets by role, not by page location.
- Keep names reusable. Avoid screen-specific labels such as `checkout hero button`.
- Use one naming pattern consistently inside the scoped area. Do not mix several patterns in the same component family.
- Keep component-set and variant names short enough to scan quickly.

## Components

- Prefer names that describe the UI role: `Button`, `Input`, `Modal`, `Tab`, `Toast`.
- If a component has subtypes, separate the base name from the subtype consistently.
- Keep component naming aligned with actual usage patterns, not temporary design explorations.

## Variants and states

- Name variants by explicit dimensions such as state, size, emphasis, or density.
- Do not hide state meaning in freeform labels.
- Keep the same order of variant dimensions within a component family.
- If one component family uses `State / Size / Tone`, do not switch another similar family to a different order without reason.

## Variables and styles

- Name by semantic role first.
- Prefer names that survive page changes and redesigns.
- Avoid names tied only to raw values when the role is already known.

## Anti-patterns

- Mixing reusable names with page-specific names in the same family
- Using several labels for the same state
- Keeping old names after a component has changed purpose
- Creating aliases or duplicates when one canonical name would be enough

## Review questions

- Can another designer find the right asset without opening it?
- Does the name describe purpose or just appearance?
- Will the name still make sense if the asset is reused elsewhere?
- Are state and variant labels explicit and consistent?
