# Figma BMAD Skill Stack

This repository contains a small Figma MCP skill stack derived from BMAD and packaged for multiple runtimes.

It is designed for work inside an existing Figma file and separates three concerns:

1. system rules
2. scoped screen composition
3. handoff readiness

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
2. `compose-screen`
3. `handoff-readiness`

If a later layer finds an upstream problem, go back instead of resolving it locally.

## Repository structure

```text
docs/
  figma-bmad/
    design-system-rules.md
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
