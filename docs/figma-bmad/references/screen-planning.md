# Screen Planning

Use this reference during `figma-bmad-prd-to-screen-plan` to guide the process of extracting a structured screen plan from product requirements.

## What screen planning is

Screen planning is the step between product requirements and screen composition. Its output is a structured planning artifact — not a Figma canvas change, not a component decision, not a system rule.

Screen planning answers:
- what views exist
- what each view is for
- what a user does in each view
- which states composition must address
- what can likely be reused
- what must be resolved before composition starts

## When planning is complete

A screen plan is complete when:

- all implied views are identified
- each view has a purpose and primary action
- critical states are listed for each view
- reuse opportunities are noted at the pattern-family level
- blockers and open questions are recorded

A screen plan is not complete when:

- views are described in layout or visual terms
- component names or variant choices have been made
- the plan attempts to pre-solve system gaps
- open questions have been answered with invented product intent

## Types of blockers to identify

Record these as pre-composition blockers when found:

- **Missing pattern family**: the required component or pattern type does not exist in the current system
- **Product ambiguity**: the requirement is too vague to define what the view should do
- **Dependency**: this view cannot be composed until another view or system decision is settled
- **Systemic gap**: the current system is inconsistent enough that composition would produce conflicting results — escalate to `figma-bmad-design-system-rules`
- **Contradiction**: two requirements or sources conflict and cannot both be honored

## Planning confidence levels

- **High**: requirements are specific, system state is known, all views map cleanly
- **Medium**: some views are inferred rather than explicit, or the system baseline is partially known
- **Low**: requirements are vague, system state is unknown, or multiple open questions remain

Low confidence does not mean the plan is wrong — it means composition should treat the plan as provisional and expect to revisit it.

## Anti-patterns

- Planning every micro-interaction and edge case instead of focusing on the view level
- Letting planning become composition by making layout or component decisions
- Collapsing two distinct user purposes into one view to reduce planning scope
- Inventing views that the requirements do not support
- Closing open questions with assumptions to keep the plan looking complete
