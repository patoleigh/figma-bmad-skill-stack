# Figma BMAD Agent Stack

This repository uses a 4-layer Figma skill stack:

1. `design-system-rules`
2. `prd-to-screen-plan`
3. `compose-screen`
4. `handoff-readiness`

Recommended order:

1. run `design-system-rules`
2. run `prd-to-screen-plan`
3. run `compose-screen`
4. run `handoff-readiness`

The Figma file is the primary evidence source. Do not replace visible file evidence with assumptions.

Escalation model:

- if `prd-to-screen-plan` finds a system gap that must be resolved before planning, escalate upstream to `design-system-rules`
- if `compose-screen` finds a system conflict, escalate upstream to `design-system-rules`
- if `handoff-readiness` finds a composition problem, escalate upstream to `compose-screen`
- if any layer finds a contradiction it cannot resolve without redefining upstream rules, stop and record the blocker instead of solving it locally

Supported runtimes:

- Codex/OpenAI via `.agents/skills/`
- Cursor via `.cursor/rules/`

Canonical documentation lives in `docs/figma-bmad/`. Runtime-specific wrappers should stay aligned to those canonical documents.

Persistent project artifacts produced by the stack:

- `Guidelines.md` — written by `design-system-rules` (optional), read by `prd-to-screen-plan` and `compose-screen`
- `planning/<feature-slug>-screen-plan.md` — written by `prd-to-screen-plan` (mandatory), read by `compose-screen`
