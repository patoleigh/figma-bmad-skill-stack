# Figma BMAD Skill Stack

This repository contains a small Figma MCP skill stack derived from BMAD and packaged for multiple runtimes.

It is designed for work inside an existing Figma file and separates four concerns:

1. system rules
2. screen planning from product requirements
3. scoped screen composition
4. handoff readiness

## What this repo contains

- canonical neutral docs in `docs/figma-bmad/`
- Codex/OpenAI skill wrappers in `.agents/skills/`
- Cursor rule wrappers in `.cursor/rules/`
- source analysis and mapping material in `docs/figma-bmad/analysis/`

## Supported runtimes

- Codex / OpenAI
- Cursor

## High-level usage

Run the stack in this order:

1. `design-system-rules`
2. `prd-to-screen-plan`
3. `compose-screen`
4. `handoff-readiness`

If a later layer finds an upstream problem, go back instead of resolving it locally.

## Repository structure

```text
docs/
  figma-bmad/
    design-system-rules.md
    prd-to-screen-plan.md
    compose-screen.md
    handoff-readiness.md
    skill-stack-overview.md
    references/
    analysis/
.agents/
  skills/
.cursor/
  rules/
AGENTS.md
README.md
```

## Canonical docs vs runtime wrappers

- `docs/figma-bmad/` is the neutral source of truth
- `.agents/skills/` contains Codex/OpenAI-oriented wrappers
- `.cursor/rules/` contains compact Cursor-oriented wrappers

The goal is to keep intent and guidance canonical in `docs/`, while letting each runtime have a thinner operational layer.
