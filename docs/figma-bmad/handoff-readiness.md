# Figma BMAD Handoff Readiness

## Purpose

Use this skill to decide whether a bounded UI scope in Figma is ready to hand to implementation without critical ambiguity.

The skill is intentionally narrow. Its job is to:

- review a concrete scope such as a screen, section, or short flow
- judge readiness from visible design evidence in the file
- classify the result as `ready`, `partial`, or `blocked`
- call out missing states, contradictions, and ambiguity that would still block implementation
- stop short of technical architecture, API design, or code review

Readiness here does not mean perfect or exhaustive. It means the scoped UI is clear enough that implementation can begin without large unresolved questions.

## Relationship to upstream skills

This skill is downstream of:

- `figma-bmad-design-system-rules`
- `figma-bmad-compose-screen`

Assume those skills have already done the following:

- system rules established or checked
- canonical source identified
- reuse-first composition applied
- local composition completed for the scoped area

This skill must not replace them.

- If the issue is really a system-rule problem, defer upstream.
- If the issue is really a composition problem, mark it as not ready rather than repairing it here.
- If the issue is deeper than the visible design artifact, do not invent implementation detail to close the gap.

## When to use

Use this skill when the task is any of the following:

- decide whether a specific screen is ready for implementation
- review a scoped UI area before handing it to development
- check whether key states, naming, and structure are clear enough
- identify whether the scope is `ready`, `partial`, or `blocked`
- find ambiguity that should be escalated before implementation starts

Read references only as needed:

- `references/readiness-checklist.md` for the core gate
- `references/ambiguity-flags.md` for common ambiguity patterns
- `references/state-coverage.md` for judging whether state coverage is sufficient
- `references/implementation-signals.md` for visible signs that the design is implementable enough

## When NOT to use

Do not use this skill when the real task is:

- redefining system rules
- composing or redesigning the screen
- writing architecture or API contracts
- reviewing code or implementation quality
- doing broad QA for an entire product
- generating missing product decisions that the file does not show

If the scope is still actively changing at the system or composition level, use the upstream skills first.

## Expected inputs

- a specific reviewed scope: screen, section, short flow, or concrete UI area
- the Figma file or scoped frames to inspect
- the most relevant reference for intent when available: requirement source, flow step, referenced screen, partial screen, or scoped update target
- the current composed result to review
- any known required states for the scope

Optional but helpful:

- the upstream rule summary from `figma-bmad-design-system-rules`
- the upstream composition summary from `figma-bmad-compose-screen`
- known platform or breakpoint expectations
- known accessibility expectations already agreed for the file

## Expected outputs

- a compact readiness assessment for the reviewed scope
- a clear status: `ready`, `partial`, or `blocked`
- a compact indication of how strong the visible evidence base is for that judgment
- explicit ready signals grounded in the visible file
- explicit partial or missing areas
- explicit blockers that still prevent handoff
- open questions that should be escalated instead of assumed away

Use this compact output shape so results stay consistent between runs:

```md
## Handoff readiness summary

- Status: [ready | partial | blocked]
- Scope reviewed: [screen/section/flow area]
- Canonical source used: [library/local/scoped pattern]
- Evidence basis: [strong visible evidence | mixed visible evidence | limited visible evidence]

## Ready signals

- [visible sign of structure, naming, system consistency, or state clarity]

## Partial or missing areas

- [important but non-blocking gap]

## Blockers

- [critical contradiction, missing state, unresolved system gap, or ambiguity]

## Open questions

- [question that should be answered before implementation if not already blocked]
```

## Core workflow

1. Confirm the reviewed scope.
   Keep the review bounded. Identify exactly which screen, section, or short flow is under review.

2. Anchor the review to upstream work.
   Use the current result as composed under `figma-bmad-design-system-rules` and `figma-bmad-compose-screen`. Do not reopen system authoring or broad composition unless a blocker forces escalation.

3. Inspect visible implementation signals.
   Review the scoped area for:
   - structure and hierarchy clarity
   - clear primary interaction
   - consistent component and variant usage
   - variable, style, and spacing consistency
   - naming that is clear enough for handoff
   - visible state coverage where the interaction requires it
   - competing sources, conflicting patterns, or contradictory signals inside the reviewed scope

4. Check minimum state coverage.
   Use `references/state-coverage.md` when the required states are not obvious. Determine whether missing states are acceptable, partial, or blocking for this scope.

5. Check ambiguity, not perfection.
   Use `references/ambiguity-flags.md` to identify implementation-risk ambiguity. Only flag what would materially confuse implementation for the reviewed scope.

6. Classify readiness.
   Use these thresholds:
   - `ready`: no critical ambiguity, no critical contradiction, and the scope is implementable from visible evidence
   - `partial`: implementable with limited clarification, and without inventing the central behavior or choosing between materially conflicting options
   - `blocked`: implementation would have to invent the central behavior, choose arbitrarily between conflicting sources, or resolve a substantial contradiction or unresolved gap

7. Summarize with a compact gate result.
   Produce the final output using the structure from `Expected outputs`.

## Decision rules

- Judge readiness from the file and the scoped design evidence, not from guessed implementation detail.
- Treat visible clarity as the default standard: structure, naming, state coverage, and system consistency should be understandable without reconstruction.
- Mark `ready` only when the scope can move to implementation without critical ambiguity.
- Use the evidence basis to show whether the judgment is grounded in strong visible evidence or limited visible evidence.
- Mark `partial` when clarification is still needed, but implementation would not need to invent the core behavior or resolve a substantial contradiction.
- Mark `blocked` when implementation would need to invent, choose arbitrarily, or reconcile substantial conflict before proceeding.
- If a problem belongs upstream to system rules or composition, do not resolve it here. Record it and downgrade readiness.
- Absence is acceptable only when the missing item is genuinely not needed for the reviewed scope. Do not assume that a missing state or signal is acceptable without evidence.
- If the same ambiguity appears across multiple parts of the reviewed scope, treat it as systemic, not local.

## Constraints

- Stay inside the reviewed scope.
- Do not repair the design as part of the readiness check.
- Do not write technical specifications the file does not support.
- Do not infer API behavior, architecture, or backend rules.
- Do not confuse visual polish issues with true handoff blockers unless they create implementation ambiguity.
- Keep the result brief, evidence-based, and comparable across runs.

## Edge cases

- The screen looks visually complete, but key interaction states are missing.
  Treat this as `partial` or `blocked` depending on whether implementation would need to guess a core behavior.

- The scope uses existing components, but naming or variant selection is unclear.
  If the ambiguity would cause implementation confusion, downgrade readiness even if the UI looks finished.

- The scope is internally coherent, but it conflicts with the canonical source or upstream rules.
  Mark the conflict explicitly. If implementation would need to choose between competing sources, treat it as `blocked`.

- The design is missing some details, but the missing details are not material for the reviewed scope.
  Keep the review narrow and do not escalate minor omissions into blockers.

- The file implies an interaction, but the structure does not show how success, error, or empty behavior should work.
  Use `references/state-coverage.md`. If one of those states is critical and absent, do not call the scope `ready`.

- A question arises that can only be answered by product or engineering decisions not visible in Figma.
  Record it under `Open questions`. If implementation cannot proceed without that answer, classify the scope as `blocked`.

## Final checklist

- Scope reviewed is explicit and bounded
- Upstream system and composition context was respected
- Structure and hierarchy are clear enough for implementation
- Primary interaction is identifiable
- Component, variant, and variable usage are consistent enough for handoff
- Naming is clear enough to avoid implementation confusion
- Required states are covered or their absence is explicitly judged
- Critical ambiguity was flagged instead of guessed away
- Readiness was classified as `ready`, `partial`, or `blocked`
- Blockers and open questions were called out explicitly
