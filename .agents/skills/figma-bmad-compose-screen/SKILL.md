---
name: figma-bmad-compose-screen
description: Codex/OpenAI wrapper for the canonical Figma BMAD compose-screen guide. Self-starting: automatically reads Guidelines.md, then planning/<feature-slug>-screen-plan.md, then inspects the live file before composing. Prompt only needs to specify which planned view to compose.
---

# Figma BMAD Compose Screen

Canonical source: `../../../docs/figma-bmad/compose-screen.md`

## Purpose

Use this wrapper to compose or update a bounded UI scope inside Codex/OpenAI.

This skill is self-starting. It does not wait to be told to read upstream artifacts. Every run begins with the automatic startup sequence before processing the view request.

## Automatic startup sequence

Run these steps at the start of every invocation, before reading the view-specific request:

**A. Read `Guidelines.md`.**
If it exists in the project repo, read it fully: active project rules, holds, and unresolved decisions. If absent, proceed with session context and label the absence in the output.

**B. Read `planning/<feature-slug>-screen-plan.md`.**
Derive the feature slug from the prompt or context. If the file exists, read it fully: views, per-view details, critical states, reuse opportunities, pre-composition blockers. If absent, fall back to scoped chat context. If neither exists, stop and surface the missing scope. Label any fallback.

**C. Identify the single target view.**
This run composes exactly one view. Identify it from the planning artifact or chat context.

**D. Inspect the live file or project files.**
Use the current Figma file or project structure as the primary visual and structural evidence source.

## Prompt contract

The prompt only needs to specify:

- which planned view to compose (name or reference)
- any decisions resolved since the planning artifact was written (optional)
- whether to apply the result or return it as a summary (optional; defaults to returning the compact output)

Do not re-state the startup sequence in the prompt. It runs automatically.

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

## Composition workflow (after startup)

1. Apply rules from `Guidelines.md` and `figma-bmad-design-system-rules`. Do not redefine them.
2. Inspect the scoped area and nearby existing patterns in the live file.
3. Build screen structure before detail, guided by the planning artifact.
4. Choose components by role, not superficial similarity.
5. Reuse variables, spacing, and layout behavior already present.
6. Check state coverage against the planning artifact's critical states list.
7. Reuse first. Extend when needed. Escalate system gaps instead of solving them locally.
8. Run basic responsive and accessibility checks when relevant.
9. Return the compact output. Label guidelines source, planning artifact source, and any degradation.

Read local references only when needed:
- `references/composition.md`
- `references/screen-structure.md`
- `references/reuse-vs-extension.md`
- `references/responsive-layout.md`

## Safe degradation

| Condition | Behavior |
|---|---|
| `Guidelines.md` missing | Proceed with session context; label absence |
| Planning artifact missing | Use scoped chat context if present; label fallback; stop if neither exists |
| Planning artifact stale or contradictory | Surface mismatch; stop if significant |
| No scope identifiable | Stop; surface blocker |

## Escalation

- If no planning artifact and no scoped chat context exist, stop and flag the missing scope.
- If the planning artifact contradicts current requirements, surface the mismatch instead of composing to a superseded plan.
- If canonical source, naming, variable, or component-family conflicts appear, defer upstream to `figma-bmad-design-system-rules`.
- If required state coverage is missing, mark the scope incomplete instead of improvising.
- If the task shifts to readiness gating, defer to `figma-bmad-handoff-readiness`.
