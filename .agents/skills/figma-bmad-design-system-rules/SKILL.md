---
name: figma-bmad-design-system-rules
description: Codex/OpenAI wrapper for the canonical Figma BMAD design-system-rules guide. Use when auditing or normalizing an existing Figma file's system rules before screen composition or handoff evaluation.
---

# Figma BMAD Design System Rules

Canonical source: `../../../docs/figma-bmad/design-system-rules.md`

## Purpose

Use this wrapper to apply the canonical design-system rule guide inside Codex/OpenAI.

This skill is the upstream rule layer for the stack. It should:

- identify the canonical source inside the current Figma file
- enforce reuse-first behavior
- normalize variables, naming, components, and layout consistency
- check responsive and accessibility basics at the system-rule level

## When to use

- before composing a new screen or section
- when canonical source is unclear
- when variables, naming, components, or variants are mixed
- when the file needs a compact, enforceable system rule summary

## When NOT to use

- full screen composition
- broad visual exploration
- deep handoff review
- product strategy, PM, or backend work

## Runtime workflow

1. Read the canonical guide at `../../../docs/figma-bmad/design-system-rules.md`.
2. Inspect only the current scoped file or area.
3. Use local reference wrappers only when needed:
   - `references/variables.md`
   - `references/naming.md`
   - `references/components.md`
   - `references/accessibility.md`
4. Produce the compact output structure defined in the canonical guide.
5. Escalate ambiguity instead of inventing system certainty.

## Escalation

- If the file has no meaningful system foundation, produce only a minimal starter rule set.
- If canonical sources compete, record the conflict instead of merging locally.
- If the task becomes screen composition, stop and defer to `figma-bmad-compose-screen`.
- If the task becomes an implementation gate, stop and defer to `figma-bmad-handoff-readiness`.
