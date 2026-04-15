---
name: figma-bmad-design-system-rules
description: Codex/OpenAI wrapper for the canonical Figma BMAD design-system-rules guide. Use when auditing or normalizing an existing Figma file's system rules before screen composition or handoff evaluation. Optionally generates or patches a project Guidelines.md when explicitly requested or when the file is empty.
---

# Figma BMAD Design System Rules

Canonical source: `../../../docs/figma-bmad/design-system-rules.md`

## Purpose

Use this wrapper to apply the canonical design-system rule guide inside Codex/OpenAI.

This skill is the upstream rule layer for the stack. It supports two modes:

- **Audit-only** (default): identify canonical source, enforce reuse-first behavior, normalize variables, naming, components, and layout consistency, check responsive and accessibility basics, and produce a compact system rule summary.
- **Audit + guidelines baseline/patch** (optional): after the audit, generate a conservative project-facing guidelines baseline or propose a targeted patch to an existing `Guidelines.md`. Activate only when explicitly requested or when `Guidelines.md` is empty.

## When to use

- before composing a new screen or section
- when canonical source is unclear
- when variables, naming, components, or variants are mixed
- when the file needs a compact, enforceable system rule summary
- when `Guidelines.md` is empty and a conservative baseline is needed
- when a patch to an existing `Guidelines.md` is requested

## When NOT to use

- full screen composition
- broad visual exploration
- deep handoff review
- product strategy, PM, or backend work
- generating guidelines when the system audit is still fully unresolved

## Runtime workflow

1. Read the canonical guide at `../../../docs/figma-bmad/design-system-rules.md`.
2. Inspect only the current scoped file or area.
3. Use local reference wrappers only when needed:
   - `references/variables.md`
   - `references/naming.md`
   - `references/components.md`
   - `references/accessibility.md`
4. Produce the compact audit output structure defined in the canonical guide.
5. Escalate ambiguity instead of inventing system certainty.
6. (Optional) If guidelines mode is active, map audit results to active rules, holds, and unresolved decisions using the guidelines output shape from the canonical guide. Never write a rule for an unresolved audit item.

## Escalation

- If the file has no meaningful system foundation, produce only a minimal starter rule set.
- If canonical sources compete, record the conflict instead of merging locally.
- If guidelines mode is requested but the system is fully unresolved, skip the guidelines output and record the blocker.
- If the task becomes screen composition, stop and defer to `figma-bmad-compose-screen`.
- If the task becomes an implementation gate, stop and defer to `figma-bmad-handoff-readiness`.
