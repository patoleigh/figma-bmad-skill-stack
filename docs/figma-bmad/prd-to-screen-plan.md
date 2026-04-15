# Figma BMAD PRD to Screen Plan

## Purpose

Use this skill to translate product requirements into a compact, structured screen plan that can feed `figma-bmad-compose-screen`.

The skill is intentionally narrow. Its job is to:

- read project guidelines from `Guidelines.md` if available, as an upstream context baseline
- read PRD-like product requirements or feature descriptions
- identify the views, screens, or bounded UI areas implied by those requirements
- define the purpose, primary actions, and critical states for each view
- identify likely reuse opportunities from the current system before composition begins
- surface gaps that must be resolved before composition can proceed cleanly
- produce a stable, repeatable output that downstream composition can use as input context
- write that output as a persistent planning artifact in the repo under `planning/`
- return the same planning output in chat

This skill does not compose screens. It does not touch the Figma canvas. It does not define or normalize system rules. It produces a planning artifact — a structured screen plan — that feeds the next layer.

Writing the planning artifact to the repo is mandatory, not optional. The persistent file is the primary handoff to `figma-bmad-compose-screen`. The chat output is a secondary convenience.

## Relationship to the stack

This skill is downstream of:

- `figma-bmad-design-system-rules`

This skill is upstream of:

- `figma-bmad-compose-screen`
- `figma-bmad-handoff-readiness`

Assume `figma-bmad-design-system-rules` has already produced a system rule summary. Use that summary to identify reuse opportunities and to flag pre-composition blockers. Do not repeat the system audit here.

If `Guidelines.md` exists in the repo, read it before planning begins. It is the stable project baseline that combines resolved design system rules and active project conventions. The guidelines file provides system context that would otherwise require re-reading the full system rule summary.

The planning artifact written by this skill becomes the primary input for `figma-bmad-compose-screen`. Composition must not start from scratch if a planning artifact already exists for the same feature scope.

This skill must not replace any other layer:

- If the task is to audit or normalize system rules, stop and defer to `figma-bmad-design-system-rules`.
- If the task is to compose a specific screen now, stop and defer to `figma-bmad-compose-screen`.
- If the task is to evaluate whether a composed screen is ready for handoff, stop and defer to `figma-bmad-handoff-readiness`.

## When to use

Use this skill when the task is any of the following:

- translating a PRD, feature brief, or product description into a set of views or screens
- identifying which scoped UI areas are implied by a set of requirements before any design work begins
- producing a stable planning input for screen composition
- deciding which views need composition first based on priority or dependency
- flagging system reuse opportunities and composition blockers before composition starts
- updating an existing planning artifact for a feature scope when requirements have changed

## When NOT to use

Do not use this skill when the real task is:

- auditing or defining system rules inside the Figma file
- composing a specific screen from existing system patterns
- reviewing a composed screen for handoff readiness
- writing product strategy, roadmaps, or PM documents
- making architectural or engineering decisions
- generating final UI from requirements in one step

Do not use this skill to jump directly from requirements to composed UI. The correct sequence is:

1. `figma-bmad-design-system-rules` → establish system rules
2. `figma-bmad-prd-to-screen-plan` → map requirements to a screen plan
3. `figma-bmad-compose-screen` → compose one specific view at a time
4. `figma-bmad-handoff-readiness` → evaluate that view for handoff

## Expected inputs

- a product requirements document, feature brief, or structured description of what the product or feature should do
- the upstream system rule summary from `figma-bmad-design-system-rules`, or a description of the current Figma system state
- `Guidelines.md` from the project repo, if it exists — used as the stable system and rule context baseline
- any known constraints: target platform, breakpoints, user roles, flow entry points

Optional but helpful:

- existing screens or flows already in the Figma file that the new work should align with
- known user journey steps or task flows
- any previously identified system gaps or component family limits
- any existing planning artifact for the same feature scope, to determine whether to update or create

## Expected outputs

This skill always produces two outputs:

1. **Chat output**: the compact screen plan returned inline in the current session.
2. **Persistent artifact**: the same content written to `planning/<feature-slug>-screen-plan.md` in the project repo.

Both outputs use the same structure. The persistent artifact is the primary handoff to `figma-bmad-compose-screen`.

Content of the output:

- a compact screen plan covering all views implied by the requirements
- a clear purpose and primary action for each view
- a list of critical states per view that composition must address
- a list of likely reuse opportunities from the current system per view
- a list of pre-composition blockers: system gaps, unresolved product decisions, or ambiguities that would prevent clean composition
- a short list of open questions for items that are too ambiguous to plan with confidence

### Planning artifact file path

Use the path: `planning/<feature-slug>-screen-plan.md`

Rules for the feature slug:

- Derive from the feature name, PRD section title, or product area — whichever is most stable and recognizable.
- Use kebab-case. Remove articles and stop words. Keep it short enough to be scannable in a file listing.
- Examples: `planning/user-authentication-screen-plan.md`, `planning/checkout-flow-screen-plan.md`, `planning/dashboard-overview-screen-plan.md`

Rules for update vs create:

- If `planning/<feature-slug>-screen-plan.md` already exists, open and update it instead of creating a new file.
- Do not create a second file for the same feature scope. A new planning run for the same scope is an update to the existing artifact, not a separate document.
- If multiple partial planning files exist for overlapping feature scopes, note the overlap in the open questions section of the new artifact. Do not silently merge them without evidence.
- If no planning file exists for the current feature, create one.

Use this compact output shape so results stay consistent between runs:

```md
## Screen plan summary

- Source: [PRD section, feature brief, or requirement description]
- Scope: [overall feature or product area]
- Total views proposed: [number]
- Planning confidence: [high | medium | low]
- Pre-composition blockers: [none | list count]

## Proposed views

| View | Purpose | Primary action |
|------|---------|----------------|
| [view name] | [what this view enables the user to do] | [the main thing a user does here] |

## Per-view detail

### [View name]

- Purpose: [what this view is for]
- Primary action: [the main user action]
- Critical states: [list the states that composition must address: default, loading, empty, error, success, disabled, or other]
- Reuse opportunities: [existing pattern families, components, or tokens likely applicable]
- Composition blockers: [system gaps, missing pattern families, or unresolved product questions]

### [next view]

...

## Cross-view considerations

- [shared patterns, navigation structures, or state dependencies that span multiple views]

## System reuse opportunities

- [patterns, components, or tokens already in the system that should anchor multiple views in this plan]

## Pre-composition blockers

- [gaps that must be resolved before compose-screen can run cleanly for any view in this plan]

## Open questions

- [product, system, or scope ambiguities that must be answered before planning or composition can proceed]
```

## Core workflow

1. Read project guidelines if available.
   Check whether `Guidelines.md` exists in the project repo. If it does, read it before planning begins. The active project rules, holds, and any documented system baseline in that file provide the rule context for reuse identification. Do not re-run the system audit here. If `Guidelines.md` does not exist, proceed using the upstream system rule summary from `figma-bmad-design-system-rules` if available.

2. Check for an existing planning artifact.
   Before creating a new file, check whether `planning/<feature-slug>-screen-plan.md` already exists for the current feature scope. If it does, the outcome of this run is an update to that file, not a new document.

3. Confirm the requirements source and scope.
   Identify the PRD section, feature brief, or product description being used. Establish the overall scope: what product area or feature set is covered. Do not plan beyond the stated scope.

4. Use upstream system rules as a reference baseline.
   If a system rule summary from `figma-bmad-design-system-rules` is available, use it alongside `Guidelines.md` to understand what pattern families, components, and tokens already exist. This informs reuse identification and blocker detection. Do not re-run the system audit here.

5. Extract the implied views from the requirements.
   Read the requirements to identify the distinct user-facing areas, screens, or bounded flow steps implied. Use `references/view-mapping.md` for guidance on how to translate product language to bounded view definitions. Do not invent views beyond what the requirements imply, and do not collapse separate concerns into a single view when the requirements suggest they serve different purposes.

6. Define purpose and primary action for each view.
   For each identified view, state: what the view enables the user to do, and what the main action is. Keep these definitions short and grounded in the requirements. Do not introduce product intent beyond what the requirements support.

7. Identify critical states per view.
   For each view, identify which interaction states are critical to its correct operation. Use `references/state-prioritization.md` to decide which states matter at the planning stage. Do not enumerate every possible state; focus on the ones that would be visibly missing at composition time.

8. Identify reuse opportunities per view and across the plan.
   For each view, identify which existing pattern families, component sets, or token groups are likely relevant. Use `references/reuse-opportunities.md` for the working approach. Note cross-view patterns that should be consistent. Do not pre-select specific component instances or make variant decisions — that belongs to composition.

9. Identify pre-composition blockers.
   For each view, and for the plan as a whole, identify what must be resolved before composition can proceed cleanly. Use `references/screen-planning.md` for the types of blockers to look for:
   - system gaps: the required pattern family does not exist in the current system
   - product ambiguity: the requirement is too vague to know what the view should do
   - dependency: this view cannot be composed until another view or system decision is settled
   - escalation: the issue should be resolved upstream in `figma-bmad-design-system-rules` before composition starts

10. Record open questions instead of inventing answers.
    If a requirement is too ambiguous to map to a confident view definition, record the open question explicitly. Do not invent views with false certainty. Do not infer product strategy beyond what the requirements state.

11. Produce the compact screen plan output and write the planning artifact.
    Assemble the final output using the structure defined in `Expected outputs`. Keep it short enough to be usable as a planning input for individual composition runs.
    - Write or update the planning artifact at `planning/<feature-slug>-screen-plan.md`.
    - If the file already exists, update it in place. Do not create a duplicate.
    - Also return the same content in chat as the session output.

## Decision rules

- Map requirements to views conservatively. When a requirement could mean one view or two, prefer fewer views and record the ambiguity.
- Define views by user purpose, not by visual layout. A view is bounded by what it enables the user to do, not by where content appears on a page.
- Keep the per-view detail planning-level, not composition-level. Purpose, action, states, and reuse opportunities — not layout, component names, or variant choices.
- Reuse identification at planning stage is directional, not prescriptive. Point toward pattern families and likely candidates. Do not commit to specific components or variants.
- Blockers surface gaps; they do not solve them. Record blockers clearly and expect them to be resolved upstream or between planning and composition.
- Open questions are evidence of appropriate uncertainty, not failure. Prefer recording an open question to filling it with invented product intent.
- Planning confidence reflects the quality of the input requirements. Low confidence does not mean the plan is wrong — it means composition should treat it as provisional.
- A view in the plan is not a composition scope. Each view in the plan will become a separate `compose-screen` run. Do not let planning become composition.

Planning artifact rules:

- The planning artifact is always written. It is not optional.
- Derive the feature slug from the feature name or PRD section title, in kebab-case.
- If the file `planning/<feature-slug>-screen-plan.md` already exists, update it. Do not create a duplicate.
- If multiple planning files exist for overlapping scopes, note the overlap in open questions. Do not merge silently.
- The content of the artifact must match the chat output exactly. There is one version, not two.

## Constraints

- Stay within the stated requirements. Do not add product features or capabilities that the requirements do not support.
- Do not compose any UI as part of this skill. The output is always a plan document, not a Figma canvas change.
- Do not define or normalize system rules. Use the upstream system summary only as a reference.
- Do not turn this into a PM framework. Screen planning is a narrow design-workflow step.
- Do not invent view names that misrepresent the requirements or over-specify product decisions.
- Do not select specific components, variants, or variable values. That belongs to `figma-bmad-compose-screen`.
- Keep the output structure compact. A screen plan that needs to be read for 20 minutes cannot practically feed composition.
- Do not attempt to plan every edge case or micro-interaction. Focus on what matters for the composition layer to start.
- Always write the planning artifact. Skipping the file write is not permitted.
- Do not create a second planning file for a scope that already has one. Update the existing file.

## Edge cases

- The requirements describe one large feature but do not suggest distinct views.
  Use the primary user actions or journey steps to infer view boundaries. If no natural boundary exists, plan it as one view and note the ambiguity.

- The requirements imply a view that has no existing system pattern family.
  Include the view in the plan, flag the missing pattern family as a pre-composition blocker, and note that `figma-bmad-design-system-rules` should address it before composition.

- The upstream system rule summary is unavailable.
  Proceed with available evidence. Note that reuse identification is lower confidence without a system baseline. Flag this in planning confidence.

- `Guidelines.md` does not exist.
  Proceed using the system rule summary from chat context if available. Note in planning confidence that the guidelines baseline was not consulted.

- Multiple requirements contradict each other.
  Do not resolve the contradiction. Record it as a pre-composition blocker and open question. Composition should not proceed until the contradiction is resolved.

- The requirements cover many views but some are clearly lower priority.
  Include all implied views in the plan, but note suggested composition order based on dependency and priority evidence in the requirements.

- The scope is too large for a single planning session.
  Divide the scope explicitly by feature area or journey segment. Plan each segment separately and note the division. Do not plan all views shallowly to cover a large scope at once.

- A view in the plan depends on another view being completed first.
  Note the dependency explicitly under cross-view considerations and composition order. Do not let the plan obscure ordering constraints.

- A planning artifact already exists for this feature scope.
  Read the existing file before starting. Update it in place based on the current run. Do not create a parallel file. Preserve unchanged sections and update only what the current requirements change.

- Multiple partial planning files exist for overlapping scopes.
  Do not silently merge them. Note the overlap in the open questions section of the new or updated artifact. Establish one canonical file path for the current scope and treat it as the primary artifact going forward.

- The scope of the new planning run is narrower than the existing planning artifact.
  Update only the relevant sections of the existing file. Label the unchanged sections as unreviewed in this run if the scope was explicitly limited.

## Final checklist

- `Guidelines.md` was read if it exists in the project repo, or the absence was noted
- Existing planning artifact for this feature scope was checked before creating a new file
- Requirements source and scope are explicitly stated
- All implied views are identified and named
- Each view has a defined purpose and primary action
- Critical states are listed per view at the planning level
- Reuse opportunities are identified per view and cross-view, at the pattern-family level
- Pre-composition blockers are listed per view and for the plan as a whole
- Open questions are recorded instead of resolved with invented product intent
- The output is planning-level only: no component selection, no layout decisions, no canvas changes
- Planning confidence is stated and reflects input quality
- The plan is compact enough to be usable as input for individual composition runs
- Planning artifact written to `planning/<feature-slug>-screen-plan.md` (created or updated)
- Chat output matches the artifact content exactly
