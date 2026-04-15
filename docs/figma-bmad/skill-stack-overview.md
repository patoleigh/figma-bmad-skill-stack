# Figma BMAD Skill Stack Overview

## Purpose of the stack

This stack provides a narrow, practical workflow for working inside an existing Figma file:

1. establish or validate system rules
2. translate product requirements into a structured screen plan
3. compose a scoped piece of UI using those rules and the screen plan
4. decide whether that scoped result is ready for implementation handoff

It does **not** try to cover the full product lifecycle. It is not a replacement for PM work, broad UX discovery, code review, architecture design, or full-product QA.

## The 4-layer model

### 1. System rules

`figma-bmad-design-system-rules` defines the rule layer for the current file:

- canonical source
- reuse-first behavior
- variables and styles
- naming
- component and variant consistency
- layout consistency
- responsive and accessibility basics

### 2. Screen planning

`figma-bmad-prd-to-screen-plan` translates product requirements into a compact screen plan that feeds composition:

- identifies the views or screens implied by the requirements
- defines purpose and primary action per view
- identifies critical states per view that composition must address
- identifies likely reuse opportunities from the current system
- surfaces pre-composition blockers and open questions

It does not compose any UI. Its output is a planning artifact only.

### 3. Screen composition

`figma-bmad-compose-screen` uses the rule layer and the screen plan to compose or update a bounded UI scope:

- screen
- section
- short flow
- scoped update area

It reuses first, extends only when needed, and escalates system problems upstream.

### 4. Handoff readiness

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
- `Guidelines.md` is empty and a conservative guidelines baseline is needed
- a patch to an existing `Guidelines.md` is requested after an audit

Do not use when:

- the real task is planning views from requirements
- the real task is composing a screen
- the real task is a handoff gate
- guidelines output is requested but the system audit is fully unresolved

Primary question:

- What rules should govern this file or scoped system area?

Optional secondary question (guidelines mode only):

- Given the audit result, which rules are resolved enough to document, which decisions should be held, and which must remain explicitly unresolved?

### `figma-bmad-prd-to-screen-plan`

Use when:

- starting design work from a PRD, feature brief, or product description
- breaking a feature into concrete named views before any Figma work begins
- identifying what states, reuse opportunities, and blockers apply to each view before composition starts
- updating an existing planning artifact after requirements change

Do not use when:

- the main problem is system-rule definition
- the task is composing a screen on the Figma canvas
- the task is handoff evaluation

Primary question:

- Given these requirements and the current system, what views should exist, what is each one for, what states matter, what can be reused, and what blocks composition?

Default behavior:

- Reads `Guidelines.md` if it exists
- Always writes the result to `planning/<feature-slug>-screen-plan.md`
- Updates the existing file for the same feature scope rather than creating a duplicate

### `figma-bmad-compose-screen`

Use when:

- a concrete screen, section, or short flow needs to be composed or updated
- a scoped UI area should be assembled from existing patterns
- a partial screen should be completed without inventing a parallel system

Do not use when:

- the main problem is system-rule definition
- views from requirements still need to be planned
- the main task is broad visual exploration
- the main task is handoff evaluation
- no planning artifact and no scoped planning context are available

Primary question:

- How should this specific UI scope be composed using the existing system?

Default behavior:

- Reads `Guidelines.md` if it exists
- Reads `planning/<feature-slug>-screen-plan.md` for the current feature scope before composing
- Composes one specific view per run
- Falls back to scoped chat context when no planning artifact exists; surfaces missing scope as a blocker if neither is available

### `figma-bmad-handoff-readiness`

Use when:

- a composed scope needs a go/no-go style implementation check
- you need to know whether a screen is `ready`, `partial`, or `blocked`
- ambiguity, missing states, or contradiction may still affect implementation

Do not use when:

- the scope still needs system-rule work
- the scope still needs screen planning or view identification
- the scope still needs composition work
- the real task is code review, architecture, or full-product QA

Primary question:

- Is this scoped UI clear enough to implement without critical ambiguity?

## Recommended order of execution

Recommended default order:

1. `figma-bmad-design-system-rules`
2. `figma-bmad-prd-to-screen-plan`
3. `figma-bmad-compose-screen`
4. `figma-bmad-handoff-readiness`

This order is not arbitrary:

- screen planning should not outrun system clarity
- composition should not start without a clear scope derived from requirements
- readiness should not evaluate a screen that is still unresolved upstream

When to go back upstream:

- from `prd-to-screen-plan` back to `design-system-rules`
  when a view requires a pattern family that does not exist and the system gap must be resolved before planning can be stable

- from `compose-screen` back to `prd-to-screen-plan`
  when the composition scope was not clearly defined or the view boundaries are unclear

- from `compose-screen` back to `design-system-rules`
  when the blocker is canonical source, system inconsistency, missing component family, naming conflict, or unresolved variable/layout rule

- from `handoff-readiness` back to `compose-screen`
  when the scope is mostly valid but still missing structure clarity, state coverage, or composition-level decisions

- from `handoff-readiness` back to upstream in general
  when implementation would have to guess because of unresolved system contradictions or missing design evidence

## Inputs and outputs between skills

The stack does not use rigid contracts, but the flow is clear.

### From `design-system-rules` to `prd-to-screen-plan`

Typical upstream outputs that help planning:

- canonical source
- existing component and pattern families
- naming conventions
- known system gaps or inconsistencies
- `Guidelines.md` if generated (project-level rule baseline)

These allow `prd-to-screen-plan` to identify reuse opportunities and blockers with more accuracy.

### From `prd-to-screen-plan` to `compose-screen`

`prd-to-screen-plan` always writes a persistent planning artifact to `planning/<feature-slug>-screen-plan.md`. This file is the primary handoff to composition.

The planning artifact contains:

- proposed views with purpose and primary action
- critical states per view
- reuse opportunities per view
- cross-view considerations
- system reuse opportunities
- pre-composition blockers
- open questions

`compose-screen` reads this file at the start of each composition run. Each view in the plan becomes a separate bounded composition scope. Composition must not begin without a planning artifact or explicitly scoped chat context.

### From `compose-screen` to `handoff-readiness`

Typical composition outputs that help readiness review:

- scoped UI summary
- structure of the screen or section
- reused assets and patterns
- extensions needed
- blocked system gaps
- open questions

`handoff-readiness` uses that context, but still judges based on visible evidence in the file.

### Project artifacts shared across the stack

Two project-level artifacts are shared across multiple skills:

- `Guidelines.md` — written by `design-system-rules`, read by `prd-to-screen-plan` and `compose-screen`
- `planning/<feature-slug>-screen-plan.md` — written by `prd-to-screen-plan`, read by `compose-screen`

### Important practical rule

Each downstream skill may use the prior skill's output, but it should not trust it blindly. The Figma file remains the primary visual evidence source. Planning artifacts and guidelines provide intent and rule context, not visual ground truth.

## Escalation model

### Escalate from `prd-to-screen-plan` to `design-system-rules` when:

- a view requires a pattern family that does not exist in the current system
- system inconsistency is severe enough that reuse identification is unreliable
- requirements conflict with the current canonical source

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

### 1. Audit the system before planning or designing new screens

1. Run `figma-bmad-design-system-rules` on the relevant library or scoped area.
2. Identify canonical source, reuse-first rules, and system gaps.
3. Only then run `figma-bmad-prd-to-screen-plan` to map requirements to views.

### 2. Plan views from a feature brief, then compose

1. Run `figma-bmad-prd-to-screen-plan` with the feature brief and the system rule summary.
2. Identify all implied views, their critical states, and likely reuse.
3. For each view in the plan, run `figma-bmad-compose-screen` individually.
4. If planning reveals a missing pattern family, escalate to `figma-bmad-design-system-rules` before composition.

### 3. Compose a new section using existing patterns

1. Start with `figma-bmad-compose-screen` if the system layer is already trusted and the scope is already defined.
2. Compose the scoped section from existing components, variants, variables, and patterns.
3. If composition finds a true system gap, escalate to `figma-bmad-design-system-rules` instead of inventing a local pattern.

### 4. Review readiness before handing to development

1. Use `figma-bmad-handoff-readiness` on the final scoped screen or section.
2. Classify as `ready`, `partial`, or `blocked`.
3. If `partial`, go back to `compose-screen` for local fixes.
4. If `blocked` because of upstream contradiction, escalate to `design-system-rules` or to the relevant non-Figma decision owner.

## Boundaries

This stack does **not** cover:

- PRD authoring or PM work
- broad visual exploration
- full product design from zero
- full product QA
- deep technical handoff
- code review
- backend, API, or architecture definition

It is specifically a Figma-side operating stack for:

- system rule clarity
- requirements-to-views planning
- scoped UI composition
- scoped handoff readiness

## Compact summary

| skill | role | primary output | escalates when |
|---|---|---|---|
| `figma-bmad-design-system-rules` | Rule layer | system rule summary for the current file or scoped area; optional guidelines baseline or patch when explicitly requested or `Guidelines.md` is empty | the file lacks enough evidence even to stabilize rules |
| `figma-bmad-prd-to-screen-plan` | Planning layer | persistent planning artifact at `planning/<feature-slug>-screen-plan.md` + same content in chat; reads `Guidelines.md` | requirements are too ambiguous, or a view requires a missing system pattern |
| `figma-bmad-compose-screen` | Composition layer | scoped screen composition summary; reads planning artifact and `Guidelines.md` before composing | the blocker is really a system gap or contradiction |
| `figma-bmad-handoff-readiness` | Readiness gate | `ready` / `partial` / `blocked` handoff summary | the scope still needs composition work or upstream rule resolution |

## Final note

This stack is intentionally narrow. It works best when each skill stays inside its own boundary:

- rules first
- planning second
- composition third
- readiness gate last

That separation is the main protection against mixing system authoring, product planning, local UI decisions, and handoff judgment into one blurred workflow.

