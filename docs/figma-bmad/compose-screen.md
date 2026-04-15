# Figma BMAD Compose Screen

## Purpose

Use this skill to compose or update a concrete UI scope inside Figma using the existing file, library, and system foundation.

The skill is intentionally narrow. Its job is to:

- read the relevant planning artifact from `planning/<feature-slug>-screen-plan.md` as the primary scope and intent input
- read project guidelines from `Guidelines.md` as the upstream rule baseline
- take a bounded UI scope such as a screen, section, or short flow
- identify which patterns and assets already exist
- compose from existing components, variants, variables, and layout rules
- extend the current system only when the scoped need cannot be solved through reuse
- keep the result coherent with the current file instead of improvising a parallel system

The planning artifact defines what this screen is for, what states it must cover, and what the system already offers. The Figma file provides the visual evidence. Guidelines provide the system rules. All three are active inputs.

This skill is downstream of the BMAD-to-Figma analysis that prioritized:

- `bmad-create-ux-design` for core experience, defining interaction, journeys, component strategy, and UX patterns
- `bmad-create-prd` for capability coverage and edge cases
- the compact, high-signal packaging pattern derived from `bmad-generate-project-context`

## Relationship to upstream skills

This skill depends on three upstream sources:

### 1. `figma-bmad-design-system-rules` — rule layer

Before composing, assume that skill has already established or validated:

- canonical source selection
- reuse-first behavior
- variable and style usage
- naming expectations
- component and variant consistency
- layout consistency
- responsive and accessibility basics

This skill must not redefine those rules. It applies them to a concrete composition task.

If composition reveals a system-level conflict, gap, or contradiction, do not silently redefine the system here. Flag the issue as a blocked or open point and, if needed, defer to `figma-bmad-design-system-rules`.

### 2. `Guidelines.md` — project baseline

If `Guidelines.md` exists in the project repo, read it before composing. It is the stable project-level rule baseline derived from the design system audit. Its active project rules govern this composition run. Its holds must be respected. Its unresolved decisions should be treated as open points, not resolved locally.

If `Guidelines.md` is absent, fall back to the system rule summary from the current session context.

### 3. `figma-bmad-prd-to-screen-plan` — planning layer

Before composing a specific view, check whether a planning artifact exists at `planning/<feature-slug>-screen-plan.md`. If it does, use it as the primary scope and intent input for this composition run. The planning artifact tells you:

- which view to compose in this run
- what the view's purpose and primary action are
- what critical states must be covered
- what the system can likely reuse
- what pre-composition blockers may still apply

If the planning artifact is missing and no scoped planning context is available in chat, escalate. Do not begin composition without knowing the intended scope and purpose of the view.

If planning context is provided directly in chat (for example, a plan pasted inline), that is an acceptable fallback when no planning file exists for the scope. Label the source explicitly in the composition output.

## When to use

Use this skill when the task is any of the following:

- compose a new screen from an already understood flow or requirement
- update an existing screen to align with the current system
- assemble a new section using patterns already present in the file or library
- complete a partial screen without creating a parallel visual language
- refine a bounded flow where the main interaction and required states are already reasonably known

Read references only as needed:

- `references/composition.md` for the composition sequence and screen-level decision order
- `references/screen-structure.md` for hierarchy, sectioning, and state coverage
- `references/reuse-vs-extension.md` for when to reuse, extend, escalate, or block
- `references/responsive-layout.md` for responsive behavior and layout consistency inside a composed screen

## When NOT to use

Do not use this skill when the real task is:

- defining or refactoring the design system itself
- inventing brand direction or new visual language
- generating many alternative visual directions
- designing a whole product from zero
- writing PM, PRD, or strategy documents
- performing deep technical handoff validation

If the task is primarily about fixing variables, naming, component rules, or canonical-source conflicts, use `figma-bmad-design-system-rules` first.

## Expected inputs

Required when available:

- the planning artifact at `planning/<feature-slug>-screen-plan.md` for the current feature scope
- `Guidelines.md` from the project repo, as the rule and system baseline
- a specific UI scope: screen, section, bounded flow, or concrete area (may be identified in the planning artifact)
- an existing Figma file with components, variants, variables, styles, or recurring local patterns

Also required:

- the relevant intent, capability, or user action the UI must support
- at least one grounding reference when available: requirement source, flow step, referenced screen, existing partial screen, or scoped update target
- any already known states the scope must cover
- any already known constraints from platform, breakpoint, accessibility, or current file structure

Optional but helpful:

- scoped planning context pasted in chat, when no planning file exists for the scope
- the journey step or flow stage this UI belongs to
- a referenced screen that already solves part of the problem
- the most relevant success path and edge case
- an existing partial screen to update rather than create from scratch
- a scoped update target inside an existing screen or section

## Expected outputs

- a compact composition summary for the scoped UI area
- an explicit list of reused assets and patterns
- a clear list of extensions needed, if any
- a short list of legitimate new asset requests, only when justified by the scoped need
- a short list of blocked system gaps or contradictions that composition should not solve locally
- open questions or unresolved ambiguities

Use this compact output shape so results stay consistent between runs:

```md
## Screen composition summary

- Scope: [screen/section/flow area]
- Primary purpose: [user goal or capability]
- Canonical source used: [library/local/scoped pattern]

## Structure

- Main sections: [header/body/sidebar/footer/panel/form/etc.]
- Primary interaction: [main user action]
- Key states covered: [default/loading/empty/error/success/etc.]

## Reused assets

- Components: [existing components or sets used]
- Variants: [existing variant axes selected]
- Variables/styles: [semantic values reused]
- Existing patterns: [layout, navigation, form, feedback, or other recurring patterns reused]

## Extensions needed

- [existing component or pattern that needs a new state, variant, or scoped adaptation]

## New assets requested

- [only if a real scoped need cannot be solved through reuse or extension; otherwise state none]

## Blocked system gaps

- [canonical source conflict, unresolved component gap, contradictory pattern, or insufficient evidence]

## Open questions

- [ambiguity, missing evidence, unresolved state, or breakpoint uncertainty]
```

## Core workflow

1. Read project guidelines.
   Check whether `Guidelines.md` exists in the project repo. If it does, read its active project rules, holds, and unresolved decisions before composing. These govern the current composition run. If it does not exist, use the system rule summary from the current session.

2. Read the planning artifact.
   Check whether `planning/<feature-slug>-screen-plan.md` exists for the current feature scope. If it does, read it and use the view definition, critical states, reuse opportunities, and pre-composition blockers from that file as the planning baseline for this composition run. If it does not exist, use planning context from chat. If neither exists, stop and surface the missing scope as a pre-composition blocker.

3. Confirm the scope and purpose.
   Using the planning artifact or chat context, define the exact UI area to compose or update. Identify the specific view from the plan being composed in this run. Keep the scope bounded to one view at a time. Identify the main user action, journey step, or capability the screen must support.

4. Anchor composition to the upstream rules.
   Use the current file according to `Guidelines.md` and the system rules from `figma-bmad-design-system-rules`. Do not start by inventing layout, components, or styles from scratch.

5. Inspect the scoped area and nearest existing patterns.
   Review the target frames or nearby screens for:
   - recurring screen structures
   - existing sections or modules that already solve similar purposes
   - components and component sets already used in similar contexts
   - variables, styles, spacing, and layout behavior already present
   - existing state handling such as loading, empty, error, success, or disabled

6. Build the screen structure before filling details.
   Use purpose and interaction flow from the planning artifact to define the main sections of the screen. Compose the hierarchy first: entry points, primary action area, supporting content, feedback zones, and any secondary controls.

7. Choose components by role, not by superficial similarity.
   Reuse the component that matches the intended purpose and behavior, not just the one that looks close. Check the nearest pattern family first: buttons, forms, navigation, feedback, loading, empty states, and search/filtering where relevant.

8. Reuse variables, spacing, and layout rules already present.
   Keep semantic variables, styles, spacing rhythm, and inferred auto layout behavior aligned with the current file. Avoid local visual exceptions unless the scoped task truly requires one.

9. Check state coverage before calling the screen complete.
   Use the critical states listed in the planning artifact as the minimum required coverage. Do not leave a pattern visually complete if its key operational states are missing.

10. Decide reuse vs extend vs escalate.
    Reuse first. Extend existing components or patterns when coverage is incomplete. If the file lacks a valid system pattern, do not improvise a new parallel pattern silently. Mark the gap as an extension request or blocked system issue.

11. Run basic responsive and accessibility checks when relevant.
    Use `references/responsive-layout.md` and, where needed, the upstream accessibility guidance already established by `figma-bmad-design-system-rules` and documented in `Guidelines.md`. Check layout consistency across repeated structures, contrast-sensitive areas, no color-only state communication, touch target basics where touch is expected, and unresolved breakpoint logic if targets are unclear.

12. Summarize the composition result.
    Produce the final output using the compact structure from `Expected outputs`. Note the planning artifact and guidelines source used.

## Decision rules

- Read the planning artifact before starting. If it exists, treat it as the primary intent and scope source for this composition run.
- Read `Guidelines.md` before starting. Its active project rules govern this run.
- Compose from existing screen and library patterns before introducing anything new.
- Choose structure from purpose and flow defined in the planning artifact, not from visual preference alone.
- Select components by role, expected behavior, and state coverage.
- Reuse variables, styles, spacing, and layout logic already present in the scoped area or canonical source.
- Extend an existing component or pattern when the system is conceptually right but missing a state, variant, or bounded adaptation.
- Escalate or block when the need is actually a system gap, not a one-off screen need.
- Stop local composition when the missing answer depends on a canonical source conflict, unresolved system contradiction, unresolved component gap, or insufficient evidence for the correct pattern.
- Keep state coverage visible. A screen is not composition-ready if the primary interaction lacks its critical states as defined in the planning artifact.
- Respect the current file's hierarchy and repetition patterns. Do not solve one local problem by breaking coherence across similar screens.
- If evidence is incomplete, preserve ambiguity explicitly instead of forcing a definitive composition rule.
- If the planning artifact is stale or contradicts the current requirements, surface the mismatch as an open point. Do not silently compose to a superseded plan.

## Constraints

- Stay inside the requested screen or bounded flow scope.
- Do not redefine system rules already owned by `figma-bmad-design-system-rules`.
- Do not create a new system language to solve a local composition task.
- Do not turn this into broad exploration of many alternatives.
- Do not introduce product features or capabilities that are not supported by the stated intent or requirement.
- Do not define technical implementation architecture.
- Do not continue expanding local composition once the real blocker is upstream, systemic, or contradictory.
- Keep the result lean, repeatable, and scoped to the current file.
- When a planning artifact exists for the feature scope, always consult it. Do not compose to an undefined or assumed scope.
- When `Guidelines.md` exists, always consult it. Do not treat system rules as unknown if they have been documented.
- The Figma file is still the primary visual evidence source. The planning artifact provides intent; the file provides implementation evidence. Neither replaces the other.

## Edge cases

- The requested screen purpose is clear, but the matching pattern family is not.
  Use the closest role-aligned pattern already present and mark the mismatch as an open point rather than inventing a new family immediately.

- A visually similar component exists, but it serves a different role.
  Do not reuse by appearance alone. Prefer a role-correct pattern or mark the gap for extension.

- The screen can be assembled only by mixing inconsistent local patterns.
  Choose the most canonical local pattern available for the scoped task and flag the inconsistency. Do not merge competing patterns into one new hybrid system.

- The main structure is easy, but a required state is missing.
  Treat this as incomplete composition. Reuse the structure, then request an extension for the missing state or variant.

- The requirement implies a capability that the current file does not visibly support.
  Do not invent a system-level solution. Mark it as a blocked gap or escalation point.

- Composition depends on a canonical source conflict, unresolved component family, or insufficient evidence for the correct pattern.
  Stop local composition at the last defensible point. Preserve reused structure if valid, then record the issue under `Blocked system gaps` or `Open questions` instead of resolving it visually.

- Responsive targets are unclear.
  Keep the composition structurally consistent and label breakpoint behavior as unresolved rather than assuming new layout rules.

- Accessibility needs affect the composed area.
  Apply only the basic composition-level checks here. If the issue is systemic, defer the rule definition upstream instead of redefining it locally.

- No planning artifact exists for the feature scope.
  If scoped planning context is available in chat, proceed using that context and label the source explicitly in the composition output. If no planning context is available at all, stop and surface the missing scope definition as a pre-composition blocker. Do not begin composition without knowing the view's purpose and primary action.

- The planning artifact exists but appears stale or contradicts the current requirements.
  Surface the mismatch as an open point. Do not compose silently to a plan that is no longer current. If the mismatch is minor and the scope is still valid, proceed with a note. If the mismatch is significant, stop and return the file to `figma-bmad-prd-to-screen-plan` for an update.

- The planning artifact covers multiple views but only one view is being composed.
  Scope this composition run to the specific view identified. Do not attempt to compose all views in a single run. Each view in the plan is a separate composition scope.

- `Guidelines.md` does not exist.
  Proceed using the system rule summary from the current session context. Note that the guidelines baseline was not consulted.

## Final checklist

- Planning artifact at `planning/<feature-slug>-screen-plan.md` was read, or its absence was noted and handled
- `Guidelines.md` was read, or its absence was noted and handled
- Scope is bounded and explicit, derived from the planning artifact or scoped chat context
- Specific view from the plan being composed in this run is identified
- Primary user action or capability is clear
- Upstream design-system rules were respected per guidelines and system audit
- Screen structure was defined before detailed styling, guided by the planning artifact
- Existing components were chosen by role and behavior
- Existing variants and states were checked before creating anything new
- Variables, styles, spacing, and layout behavior stay aligned with the current file
- Key interaction states were covered or explicitly marked missing, measured against the planning artifact's critical states list
- Responsive behavior was checked at a basic composition level where relevant
- No local workaround created a parallel system pattern
- Extensions, blocked gaps, and open questions were called out explicitly
- Planning artifact and guidelines source noted in the composition output
