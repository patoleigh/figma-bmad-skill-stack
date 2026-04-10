---
name: figma-bmad-compose-screen
description: Codex/OpenAI wrapper for the canonical Figma BMAD compose-screen guide. Use when composing or updating a bounded screen, section, or short flow inside an existing Figma file by reusing the current system first.
---

# Figma BMAD Compose Screen

Canonical source: `../../../docs/figma-bmad/compose-screen.md`

## Purpose

Use this wrapper to compose or update a bounded UI scope inside Codex/OpenAI while staying downstream of `figma-bmad-design-system-rules`.

This skill should:

- keep the scope concrete and local
- choose patterns and components by role
- reuse variables, variants, and layout behavior already present
- extend only when needed
- stop when the problem is actually systemic or upstream

## When to use

- composing a new screen from an already understood flow or requirement
- updating an existing screen to align with the current system
- assembling a section from patterns already present
- completing a partial screen without inventing a parallel language

## When NOT to use

- defining system rules
- broad visual exploration
- full-product design
- deep technical handoff validation

## Runtime workflow

1. Read `../../../docs/figma-bmad/compose-screen.md`.
2. Assume upstream rule guidance from `figma-bmad-design-system-rules` is active.
3. Read local references only when needed:
   - `references/composition.md`
   - `references/screen-structure.md`
   - `references/reuse-vs-extension.md`
   - `references/responsive-layout.md`
4. Compose from existing patterns first.
5. Produce the compact output structure defined in the canonical guide.
6. Escalate blocked system gaps instead of solving them locally.

## Escalation

- If canonical source, naming, variable, or component-family conflicts appear, defer upstream.
- If required state coverage is missing, mark the scope incomplete instead of improvising.
- If the task shifts to readiness gating, defer to `figma-bmad-handoff-readiness`.
