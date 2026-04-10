# Figma BMAD Agent Stack

This repository uses a 3-layer Figma skill stack:

1. `design-system-rules`
2. `compose-screen`
3. `handoff-readiness`

Recommended order:

1. run `design-system-rules`
2. run `compose-screen`
3. run `handoff-readiness`

The Figma file is the primary evidence source. Do not replace visible file evidence with assumptions.

Escalation model:

- if `compose-screen` finds a system conflict, escalate upstream to `design-system-rules`
- if `handoff-readiness` finds a composition problem, escalate upstream to `compose-screen`
- if any layer finds a contradiction it cannot resolve without redefining upstream rules, stop and record the blocker instead of solving it locally

Supported runtimes:

- Codex/OpenAI via `.agents/skills/`
- Cursor via `.cursor/rules/`

Canonical documentation lives in `docs/figma-bmad/`. Runtime-specific wrappers should stay aligned to those canonical documents.
