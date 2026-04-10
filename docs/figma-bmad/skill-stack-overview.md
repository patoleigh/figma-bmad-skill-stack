# Figma BMAD Skill Stack Overview

## Purpose of the stack

This stack provides a narrow, practical workflow for working inside an existing Figma file:

1. establish or validate system rules
2. compose a scoped piece of UI using those rules
3. decide whether that scoped result is ready for implementation handoff

It does **not** try to cover the full product lifecycle. It is not a replacement for PM work, broad UX discovery, code review, architecture design, or full-product QA.

## The 3-layer model

### 1. System rules

`figma-bmad-design-system-rules` defines the rule layer for the current file:

- canonical source
- reuse-first behavior
- variables and styles
- naming
- component and variant consistency
- layout consistency
- responsive and accessibility basics

### 2. Screen composition

`figma-bmad-compose-screen` uses that rule layer to compose or update a bounded UI scope:

- screen
- section
- short flow
- scoped update area

It reuses first, extends only when needed, and escalates system problems upstream.

### 3. Handoff readiness

`figma-bmad-handoff-readiness` evaluates whether that scoped result is clear enough to move to implementation without critical ambiguity.

It does not repair the design. It acts as a readiness gate and classifies the scope as:

- `ready`
- `partial`
- `blocked`

## When to use each skill

### `figma-bmad-design-system-rules`

Use when:

- the file needs a system-rule audit
- canonical source is unclear
- variables, naming, components, or consistency need normalization
- responsive or accessibility basics need to be checked at the system level

Do not use when:

- the real task is composing a screen
- the real task is a handoff gate

Primary question:

- What rules should govern this file or scoped system area?

### `figma-bmad-compose-screen`

Use when:

- a concrete screen, section, or short flow needs to be composed or updated
- a scoped UI area should be assembled from existing patterns
- a partial screen should be completed without inventing a parallel system

Do not use when:

- the main problem is system-rule definition
- the main task is broad visual exploration
- the main task is handoff evaluation

Primary question:

- How should this specific UI scope be composed using the existing system?

### `figma-bmad-handoff-readiness`

Use when:

- a composed scope needs a go/no-go style implementation check
- you need to know whether a screen is `ready`, `partial`, or `blocked`
- ambiguity, missing states, or contradiction may still affect implementation

Do not use when:

- the scope still needs system-rule work
- the scope still needs composition work
- the real task is code review, architecture, or full-product QA

Primary question:

- Is this scoped UI clear enough to implement without critical ambiguity?

## Recommended order of execution

Recommended default order:

1. `figma-bmad-design-system-rules`
2. `figma-bmad-compose-screen`
3. `figma-bmad-handoff-readiness`

This order is not arbitrary:

- composition should not outrun system clarity
- readiness should not evaluate a screen that is still unresolved upstream

When to go back upstream:

- from `compose-screen` back to `design-system-rules`
  when the blocker is canonical source, system inconsistency, missing component family, naming conflict, or unresolved variable/layout rule

- from `handoff-readiness` back to `compose-screen`
  when the scope is mostly valid but still missing structure clarity, state coverage, or composition-level decisions

- from `handoff-readiness` back to upstream in general
  when implementation would have to guess because of unresolved system contradictions or missing design evidence

## Inputs and outputs between skills

The stack does not use rigid contracts, but the flow is clear.

### From `design-system-rules` to `compose-screen`

Typical upstream outputs that help composition:

- canonical source
- reuse/extend decisions
- naming expectations
- variable and style expectations
- component and variant constraints
- layout and responsive/accessibility basics

These can be used as explicit input or simply as the assumed rule layer for composition.

### From `compose-screen` to `handoff-readiness`

Typical composition outputs that help readiness review:

- scoped UI summary
- structure of the screen or section
- reused assets and patterns
- extensions needed
- blocked system gaps
- open questions

`handoff-readiness` uses that context, but still judges based on visible evidence in the file.

### Important practical rule

Each downstream skill may use the prior skill's summary, but it should not trust the summary blindly. The file itself remains the main evidence source.

## Escalation model

### Escalate from `compose-screen` to `design-system-rules` when:

- canonical source is unclear
- component families conflict
- naming inconsistency is systemic
- variables/styles are too inconsistent to support safe composition
- the needed solution is really a system gap, not a local screen need

### Escalate from `handoff-readiness` to `compose-screen` when:

- the screen structure is still unclear
- key states are missing for the scoped interaction
- the primary interaction is not clear enough
- the screen is mostly understandable but still needs local composition clarification

### Escalate upstream more broadly when:

- implementation would need to invent core behavior
- the file presents competing sources or contradictory patterns
- a blocker depends on product or engineering decisions not visible in Figma

Working principle:

- no skill should solve more than its layer owns
- when the problem is upstream, stop and escalate instead of compensating locally

## Example usage flows

### 1. Audit the system before designing a new screen

1. Run `figma-bmad-design-system-rules` on the relevant library or scoped area.
2. Identify canonical source, reuse-first rules, and system gaps.
3. Only then run `figma-bmad-compose-screen` for the new screen.

### 2. Compose a new section using existing patterns

1. Start with `figma-bmad-compose-screen` if the system layer is already trusted.
2. Compose the scoped section from existing components, variants, variables, and patterns.
3. If composition finds a true system gap, escalate to `figma-bmad-design-system-rules` instead of inventing a local pattern.

### 3. Review readiness before handing to development

1. Use `figma-bmad-handoff-readiness` on the final scoped screen or section.
2. Classify as `ready`, `partial`, or `blocked`.
3. If `partial`, go back to `compose-screen` for local fixes.
4. If `blocked` because of upstream contradiction, escalate to `design-system-rules` or to the relevant non-Figma decision owner.

## Boundaries

This stack does **not** cover:

- PRD or PM work
- broad visual exploration
- full product design from zero
- full product QA
- deep technical handoff
- code review
- backend, API, or architecture definition

It is specifically a Figma-side operating stack for:

- system rule clarity
- scoped UI composition
- scoped handoff readiness

## Compact summary

| skill | role | primary output | escalates when |
|---|---|---|---|
| `figma-bmad-design-system-rules` | Rule layer | system rule summary for the current file or scoped area | the file lacks enough evidence even to stabilize rules |
| `figma-bmad-compose-screen` | Composition layer | scoped screen composition summary | the blocker is really a system gap or contradiction |
| `figma-bmad-handoff-readiness` | Readiness gate | `ready` / `partial` / `blocked` handoff summary | the scope still needs composition work or upstream rule resolution |

## Final note

This stack is intentionally narrow. It works best when each skill stays inside its own boundary:

- rules first
- composition second
- readiness gate last

That separation is the main protection against mixing system authoring, local UI decisions, and handoff judgment into one blurred workflow.
