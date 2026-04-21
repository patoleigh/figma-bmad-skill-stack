---
name: figma-bmad-mockup-to-requirements
description: Codex/OpenAI wrapper for the canonical Figma BMAD mockup-to-requirements guide. Use when reconstructing requirements from existing mockups that lack documented product requirements. Always writes a persistent requirements draft to requirements/<feature-slug>-requirements-draft.md.
---

# Figma BMAD Mockup to Requirements

Canonical source: `../../../docs/figma-bmad/mockup-to-requirements.md`

## Purpose

Use this wrapper to recover requirements from existing Figma mockups inside Codex/OpenAI.

This skill is an **auxiliary recovery tool**, not part of the default workflow. It reconstructs requirements from visible design evidence when the original requirements are missing or were never documented.

The skill produces a **requirements draft grounded in visible design evidence**, not a final PRD. Writing the requirements artifact is mandatory.

## Position in the stack

This skill is an **alternative entry point** when requirements are missing.

- **Feeds into**: `figma-bmad-prd-to-screen-plan`
- **Not part of**: the default happy-path workflow
- **May consult**: `figma-bmad-design-system-rules` or `Guidelines.md` to distinguish system conventions from product requirements

## When to use

- a mockup exists but requirements were never written down
- legacy designs need to be reverse-documented
- requirements need to be reconstructed before planning/composition can proceed
- a team wants to recover product intent from existing mockups

## When NOT to use

- starting with known product requirements (use `figma-bmad-prd-to-screen-plan` directly)
- auditing or defining system rules
- composing screens or sections
- evaluating handoff readiness
- inventing product strategy where no design evidence exists

## Runtime workflow

1. Read the canonical guide at `../../../docs/figma-bmad/mockup-to-requirements.md`.
2. Read `Guidelines.md` if it exists in the project repo, to understand system-level conventions.
3. Optionally consult the system rule summary from `figma-bmad-design-system-rules` if available.
4. Analyze the specified Figma mockup, screen, or selection.
5. Use local reference wrappers only when needed:
   - `references/visual-evidence-extraction.md`
   - `references/requirements-inference.md`
   - `references/assumptions-and-gaps.md`
6. Extract visible evidence systematically.
7. Infer requirements conservatively, separating evidence, inference, assumptions, and open questions.
8. Distinguish product requirements from system conventions.
9. Produce the compact output structure defined in the canonical guide.
10. Write or update `requirements/<feature-slug>-requirements-draft.md`. Do not create a duplicate if a file already exists for this scope.
11. Return the same requirements draft in chat.

## Critical constraints

- Stay grounded in visible design evidence. Do not fabricate product strategy or deep business logic with false certainty.
- Separate observed evidence, inferred requirements, assumptions, and open questions explicitly.
- Do not generate a full PRD for an entire product if only one view is shown.
- Do not compose new screens, redefine system rules, or perform handoff evaluation.
- Do not invent backend, API, or architecture contracts.
- Always write the requirements artifact. Skipping the file write is not permitted.
- Do not create a second requirements file for a scope that already has one. Update the existing file.

## Escalation

- If the mockup provides too limited evidence to infer confident requirements, produce a low-confidence draft and note the limited evidence basis.
- If the mockup conflicts with known system conventions, note the conflict explicitly. Do not treat it as a product requirement without validation.
- If the task shifts to screen planning, stop and defer to `figma-bmad-prd-to-screen-plan`.
- If the task shifts to screen composition, stop and defer to `figma-bmad-compose-screen`.
- If the task shifts to handoff evaluation, stop and defer to `figma-bmad-handoff-readiness`.
