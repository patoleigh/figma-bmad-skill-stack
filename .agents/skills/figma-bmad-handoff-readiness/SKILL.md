---
name: figma-bmad-handoff-readiness
description: Codex/OpenAI wrapper for the canonical Figma BMAD handoff-readiness guide. Use when evaluating whether a bounded Figma scope is ready for implementation without critical ambiguity.
---

# Figma BMAD Handoff Readiness

Canonical source: `../../../docs/figma-bmad/handoff-readiness.md`

## Purpose

Use this wrapper to run a narrow readiness gate inside Codex/OpenAI after system rules and composition are already in place.

This skill should:

- inspect only visible design evidence in the reviewed scope
- classify readiness as `ready`, `partial`, or `blocked`
- distinguish limited clarification from true implementation blockers
- surface ambiguity instead of closing gaps with assumptions

## When to use

- deciding whether a screen, section, or short flow is ready for implementation
- checking naming, state coverage, and structure before handoff
- identifying ambiguity that should be escalated before engineering starts

## When NOT to use

- redefining system rules
- composing or repairing the screen
- writing architecture or API contracts
- reviewing code

## Runtime workflow

1. Read `../../../docs/figma-bmad/handoff-readiness.md`.
2. Assume upstream outputs from `figma-bmad-design-system-rules` and `figma-bmad-compose-screen`.
3. Use local references only when needed:
   - `references/readiness-checklist.md`
   - `references/ambiguity-flags.md`
   - `references/state-coverage.md`
   - `references/implementation-signals.md`
4. Judge readiness from visible file evidence only.
5. Produce the compact output structure defined in the canonical guide.
6. Escalate upstream problems instead of resolving them here.

## Escalation

- If the blocker is systemic, defer to `figma-bmad-design-system-rules`.
- If the blocker is composition-level, defer to `figma-bmad-compose-screen`.
- If implementation would need to invent central behavior or choose between conflicting sources, mark the scope `blocked`.
