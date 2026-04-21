# Figma BMAD Skill Stack

This repository contains a small Figma MCP skill stack derived from BMAD and packaged for multiple runtimes.

It is designed for work inside an existing Figma file and separates four concerns:

1. system rules
2. screen planning from product requirements
3. scoped screen composition
4. handoff readiness

Plus one auxiliary skill for recovering requirements when they are missing:

- mockup-to-requirements (alternative entry point)

## What this repo contains

- canonical neutral docs in `docs/figma-bmad/`
- Codex/OpenAI skill wrappers in `.agents/skills/`
- Cursor rule wrappers in `.cursor/rules/`
- source analysis and mapping material in `docs/figma-bmad/analysis/`

## Supported runtimes

- Codex / OpenAI
- Cursor

## High-level usage

Run the stack in this order (happy path):

1. `design-system-rules`
2. `prd-to-screen-plan`
3. `compose-screen`
4. `handoff-readiness`

If requirements are missing, use the recovery path:

1. `mockup-to-requirements`
2. Validate the requirements draft with stakeholders
3. `prd-to-screen-plan`
4. `compose-screen`
5. `handoff-readiness`

If a later layer finds an upstream problem, go back instead of resolving it locally.

## Repository structure

```text
docs/
  figma-bmad/
    design-system-rules.md
    prd-to-screen-plan.md
    compose-screen.md
    handoff-readiness.md
    mockup-to-requirements.md
    skill-stack-overview.md
    references/
    analysis/
.agents/
  skills/
.cursor/
  rules/
requirements/
planning/
AGENTS.md
README.md
```

## Canonical docs vs runtime wrappers

- `docs/figma-bmad/` is the neutral source of truth
- `.agents/skills/` contains Codex/OpenAI-oriented wrappers
- `.cursor/rules/` contains compact Cursor-oriented wrappers

The goal is to keep intent and guidance canonical in `docs/`, while letting each runtime have a thinner operational layer.

## Pasos

### Paso 1

Use this Figma file/selection:
[pega aquí el link]

Use figma-bmad-design-system-rules on the relevant scoped area.
Do not compose new UI yet.
Return the compact output structure from the stack.


### Paso 2

Use figma-bmad-mockup-to-requirements.

Use these inputs in this order:

Guidelines.md
the current Figma file/selection as visual evidence
the small context I provide below

Your task:
Analyze the current mockup/screen and generate a structured requirements draft based on:

what is directly visible
what can be inferred with reasonable confidence
what must remain an assumption
what is still unknown and should be asked

Important:

Do not invent product truth where the design is ambiguous
Do not compose new UI
Do not redefine the design system
Do not generate backend or API contracts
Keep the output compact, structured, and useful for later feeding into figma-bmad-prd-to-screen-plan
Persist the requirements draft in the project artifact path if the skill supports it

Small context:
[paste here your short context, for example:
“This screen is part of the user management flow for admins. It is intended for bulk operations on users.”]

Return:

Requirements draft summary
Screen purpose
Likely user goal
Primary actions
Secondary actions
Visible / implied states
Inferred business rules
Validation / constraint hints
Assumptions made
Missing requirements / open questions