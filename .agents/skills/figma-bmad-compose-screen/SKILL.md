---
name: figma-bmad-compose-screen
description: Codex/OpenAI wrapper for the canonical Figma BMAD compose-screen guide. Use when composing or updating a bounded screen, section, or short flow inside an existing Figma file. Reads planning/\<feature-slug\>-screen-plan.md and Guidelines.md as primary upstream inputs before composing.
---

# Figma BMAD Compose Screen

Canonical source: `../../../docs/figma-bmad/compose-screen.md`

## Purpose

Use this wrapper to compose or update a bounded UI scope inside Codex/OpenAI.

This skill reads three upstream sources before composing:

1. `Guidelines.md` — the project rule baseline (active rules, holds, unresolved decisions)
2. `planning/<feature-slug>-screen-plan.md` — the planning artifact for the feature scope (view purpose, states, reuse, blockers)
3. The Figma file — the visual evidence source for patterns and system state

It should:

- read guidelines and the planning artifact before starting
- keep the scope concrete and local (one view per run)
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
- when no planning artifact and no scoped context are available

## Runtime workflow

1. Read `../../../docs/figma-bmad/compose-screen.md`.
2. Read `Guidelines.md` if it exists in the project repo.
3. Read `planning/<feature-slug>-screen-plan.md` if it exists for the current feature scope. If it does not exist, use scoped chat context. If neither exists, surface the missing scope as a blocker.
4. Assume upstream rule guidance from `figma-bmad-design-system-rules` is active.
5. Read local references only when needed:
   - `references/composition.md`
   - `references/screen-structure.md`
   - `references/reuse-vs-extension.md`
   - `references/responsive-layout.md`
6. Compose one specific view from the planning artifact per run.
7. Produce the compact output structure defined in the canonical guide. Note the planning artifact and guidelines source used.
8. Escalate blocked system gaps instead of solving them locally.

## Escalation

- If no planning artifact and no scoped chat context exist, stop and flag the missing scope definition.
- If the planning artifact is stale or contradicts current requirements, surface the mismatch instead of composing to a superseded plan.
- If canonical source, naming, variable, or component-family conflicts appear, defer upstream.
- If required state coverage is missing, mark the scope incomplete instead of improvising.
- If the task shifts to readiness gating, defer to `figma-bmad-handoff-readiness`.
