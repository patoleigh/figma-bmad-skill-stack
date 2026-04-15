---
name: figma-bmad-prd-to-screen-plan
description: Codex/OpenAI wrapper for the canonical Figma BMAD prd-to-screen-plan guide. Use when translating PRD-like product requirements into a compact, structured screen plan that feeds figma-bmad-compose-screen. Always writes a persistent planning artifact to planning/<feature-slug>-screen-plan.md.
---

# Figma BMAD PRD to Screen Plan

Canonical source: `../../../docs/figma-bmad/prd-to-screen-plan.md`

## Purpose

Use this wrapper to run the screen planning step inside Codex/OpenAI.

This skill sits between `figma-bmad-design-system-rules` and `figma-bmad-compose-screen`. It should:

- read `Guidelines.md` if it exists, as the upstream project rule baseline
- read product requirements and map them to bounded views
- define purpose, primary action, and critical states per view
- identify likely reuse opportunities from the current system
- surface pre-composition blockers and open questions
- write the planning output to `planning/<feature-slug>-screen-plan.md` (always)
- return the same plan in chat

Writing the planning artifact is mandatory. It is the primary handoff to `figma-bmad-compose-screen`.

## When to use

- before composing any screen when starting from product requirements
- when a feature brief needs to be broken into concrete view scopes
- when composition order or dependencies must be established before Figma work begins
- when updating an existing planning artifact after requirements change

## When NOT to use

- auditing or normalizing system rules
- composing a specific screen on the Figma canvas
- evaluating handoff readiness
- writing product strategy or technical specifications

## Runtime workflow

1. Read `../../../docs/figma-bmad/prd-to-screen-plan.md`.
2. Read `Guidelines.md` if it exists in the project repo.
3. Check whether `planning/<feature-slug>-screen-plan.md` already exists for this scope.
4. Assume upstream rule guidance from `figma-bmad-design-system-rules` is available. Use it alongside guidelines as the system baseline for reuse identification.
5. Read local references only when needed:
   - `references/screen-planning.md`
   - `references/view-mapping.md`
   - `references/state-prioritization.md`
   - `references/reuse-opportunities.md`
6. Map requirements to views conservatively. Record open questions instead of inventing views with false certainty.
7. Produce the compact output structure defined in the canonical guide.
8. Write or update `planning/<feature-slug>-screen-plan.md`. Do not create a duplicate if a file already exists for this scope.
9. Do not compose any UI. Output is a planning artifact only.

## Escalation

- If requirements are too ambiguous to map to views, record open questions instead of inventing views.
- If a view depends on a system pattern family that does not exist, flag as a pre-composition blocker and escalate to `figma-bmad-design-system-rules`.
- If system conflicts found during planning would affect multiple views, surface them as cross-view blockers.
- If the task shifts to screen composition, stop and defer to `figma-bmad-compose-screen`.
- If the task shifts to handoff review, stop and defer to `figma-bmad-handoff-readiness`.
