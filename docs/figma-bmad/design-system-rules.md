# Figma BMAD Design System Rules

## Purpose

Use this skill to turn an existing or partial Figma design system into a short set of enforceable working rules.

The skill is intentionally narrow. Its job is to:

- inspect the current system foundation
- prefer reuse over net-new creation
- normalize variables, naming, and component decisions
- catch basic consistency, responsive, and accessibility issues

It supports two output modes:

- **Audit-only** (default): produces the compact system rule summary. No guidelines file is generated or modified.
- **Audit + guidelines baseline/patch** (optional): after the audit, generates or proposes an update to a project-facing guidelines document. This mode is active only when explicitly requested, or when the project guidelines file is empty and the audit evidence is sufficient for a conservative baseline.

The guidelines output is always grounded in the audit result. It never fabricates resolved decisions, never silently merges conflicting canonical sources, and never writes authoritative rules where the evidence is incomplete.

This skill is based primarily on the BMAD material mapped as portable from:

- `bmad-create-ux-design` design system, visual foundation, component strategy, UX patterns, and responsive/accessibility
- `bmad-generate-project-context` compact rule packaging
- selected consistency ideas from `bmad-create-architecture`

Inference note:

- "Auto layout" rules are a prudent Figma translation of BMAD spacing, layout foundation, structure, and consistency patterns. The source material does not name Figma auto layout directly.
- Some naming guidance is also a prudent translation from BMAD naming and consistency patterns into Figma-friendly conventions.

## When to use

Use this skill when the task is any of the following:

- audit an existing Figma file for design system consistency
- decide whether to reuse, extend, or create a component
- normalize or validate variables, styles, and token usage
- check naming consistency across components, variants, or variables
- review a partial library before more design work continues
- verify basic responsive and accessibility readiness at the system-rule level
- create a compact rule set for how the Figma system should be used going forward
- generate a conservative baseline `Guidelines.md` when the project guidelines file is empty
- propose a patch to an existing `Guidelines.md` without overwriting unresolved system decisions

Read references only as needed:

- `references/variables.md` for token and style normalization
- `references/naming.md` for naming cleanup or new asset naming
- `references/components.md` for reuse, variants, states, and custom component decisions
- `references/accessibility.md` for contrast basics, no color-only state communication, touch target basics, and responsive consistency checks

## When NOT to use

Do not use this skill when the real task is:

- designing a full product from scratch
- composing complete screens or flows
- generating many visual directions
- writing a PRD or broad product strategy
- making backend, infrastructure, or deployment decisions
- performing a deep developer handoff audit across code and architecture

If the file has no meaningful system foundation at all, this skill can only produce a minimal rule starter. It should not pretend a mature system already exists.

## Expected inputs

- a Figma file with an existing library, partial library, or local system foundation
- available variables, styles, components, or component sets
- known brand constraints if they already exist
- any explicit project rules already documented
- the specific scope to audit or normalize, if provided

Optional but helpful:

- known breakpoints or platform targets
- known accessibility targets
- known component gaps already identified by the team

## Expected outputs

### Audit-only output (always produced)

- a compact, explicit rule set for using the design system inside the current file
- a decision for each reviewed area: reuse, extend, normalize, or create new
- a short list of unresolved gaps or ambiguities
- a basic readiness check for variables, components, responsiveness, and accessibility

Use this compact output shape so results stay consistent between runs:

```md
## System rule summary

- Canonical source: [library/local mix/scoped area]
- Scope reviewed: [frames, pages, component families, or target area]

## Decisions

- Variables/styles: [reuse | normalize | extend | unresolved]
- Naming: [stable | partially mixed | unresolved]
- Components: [reuse | extend | create only where justified]
- Layout consistency: [stable | mixed | unresolved]
- Responsive/accessibility basics: [pass | partial | unresolved]

## Actions

- Reuse: [assets or patterns to keep using]
- Normalize: [items to align now]
- Extend: [existing assets that need states/variants]
- Hold: [things not to create yet]

## Open points

- [ambiguity, conflict, or missing evidence]
```

### Guidelines baseline/patch output (optional)

Produced only when:

- explicitly requested, or
- the project guidelines file is empty and the audit has enough resolved evidence for a conservative baseline

Use this shape for the guidelines output:

```md
## Guidelines baseline

### Active project rules
[Only resolved, evidence-backed rules. Each rule must be traceable to audit findings.]

### Holds — do not expand yet
[Patterns, components, or decisions to defer. Include the reason.]

### Unresolved decisions
[System conflicts, competing canonical sources, or open team decisions that cannot be resolved from file evidence alone. These must not be promoted to active rules.]

### Suggested patch for Guidelines.md
[Only when Guidelines.md already exists. List additions or revisions to specific sections. Never replace the full file; propose targeted updates only.]
```

Guidelines output rules:

- Only resolved rules from the audit may be written as active project rules.
- Unresolved system conflicts must remain explicitly listed as unresolved decisions, not collapsed into a rule.
- When evidence is mixed or the canonical source is still in conflict, produce only a conservative baseline. Do not invent a final rule set.
- If `Guidelines.md` already exists and is non-empty, produce a patch proposal. Do not blindly replace the file.
- If the system is fully unresolved, do not produce a guidelines output at all. Record the blocker and stop.

## Core workflow

1. Inspect the current foundation.
   Identify what already exists inside the scoped file or area:
   - enabled libraries
   - local components and component sets
   - variables and collections
   - styles
   - visible naming patterns
   - repeated patterns in the target frames or other scoped areas
   - repeated spacing, container, and layout behavior that likely act as system rules

2. Establish the canonical source.
   Decide which assets are the system source of truth for the current task. If there are duplicates or conflicting sources, do not merge them silently.

3. Check variables and styles first.
   Verify whether color, text, spacing, and other repeated values are already represented semantically. Prefer existing variables/styles over local hardcoded values.

4. Check naming before creation.
   Review how components, variants, and variables are named. Keep the minimum Figma-native rules active in the scoped area:
   - components named by object or purpose
   - variants named by property axis such as state, size, emphasis, or density
   - avoid page or frame prefixes unless there is a clear operational reason
   If naming is mixed, choose one scoped pattern first and flag deviations before expanding the system further.

5. Check component coverage.
   Compare what the file already has against what the system needs at the rule level: base components, expected states, variants, and repeated patterns.

6. Decide reuse vs extend vs create.
   Prefer reuse first. Extend an existing component if the pattern already exists but coverage is incomplete. Create a new component only when the current system cannot express the needed purpose without distortion.

7. Check layout consistency.
   Treat recurring spacing and container structure as system rules. In Figma terms, prefer consistent auto layout behavior where repeated UI structures exist. This step is inferred from BMAD layout-foundation material.

8. Run basic responsive and accessibility checks.
   Use `references/accessibility.md` when the task touches accessibility or responsive behavior. At minimum check:
   - contrast basics on semantic colors and common text usage
   - no color-only state communication
   - touch target basics where touch interaction is expected
   - responsive behavior consistency across repeated patterns
   - unresolved breakpoint logic when breakpoint targets are not clear

9. Summarize the system rule outcome.
   Produce the final output using the compact structure from `Expected outputs`.

10. (Optional) Generate or patch project guidelines.
    Only when explicitly requested, or when `Guidelines.md` is empty and the audit evidence is sufficient:
    - Map audit decisions to active project rules, holds, and unresolved decisions.
    - Write active project rules only for items where the audit reached a clear, evidence-backed conclusion.
    - List holds explicitly with the reason for deferral.
    - List unresolved decisions explicitly. Do not resolve them in this step.
    - If `Guidelines.md` already exists and has content, produce a targeted patch proposal only. Do not replace the file.
    - If the system is fully unresolved, skip this step entirely and note the blocker.

## Decision rules

- Reuse an existing library component if it already matches the purpose, pattern, and required state coverage closely enough.
- Extend an existing component when the core pattern is already correct but a missing state, size, or variant prevents consistent use.
- Create a new component only when no existing component expresses the purpose without breaking the current system.
- Prefer semantic variables and styles over local values. If a value repeats or represents a system role, it should not stay ad hoc.
- Map colors by role, not by page-specific usage. The same principle applies to text, spacing, and other repeated design decisions.
- Keep component naming role-based and reusable. Avoid names tied to one screen or one temporary context.
- Name components by object or purpose, not by page placement.
- Keep variant names short and explicit. State, size, emphasis, and density should be discoverable without opening the component.
- Name variants by property axis. Avoid freeform labels when a reusable axis already exists.
- Avoid page or frame prefixes unless they solve a real ambiguity in the scoped file.
- Keep spacing and layout patterns consistent. If the same structure appears multiple times, it should follow the same container logic and spacing rhythm.
- Treat accessibility and responsive basics as system rules, not as optional cleanup.
- If evidence is weak or the current file is inconsistent, document the ambiguity instead of inventing certainty.

Guidelines-specific decision rules:

- Only audit-resolved items may be written as active project rules in the guidelines output.
- Any item that remains in the audit's "open points" must appear in the guidelines output as an unresolved decision, not as a rule.
- When the canonical source is still in conflict, do not generate a guidelines output. Record the blocker.
- When evidence is mixed, produce a conservative baseline that documents what is known and explicitly labels what is not.
- Do not fabricate a final design system decision to fill a gap in the guidelines. A missing decision is better than a false one.
- If `Guidelines.md` exists and is non-empty, propose a patch. Never replace the full document blindly.

## Constraints

- Stay inside the current design-system scope.
- Favor normalization and reuse before expansion.
- Do not redesign the product or invent new product flows.
- Do not replace brand choices unless the task explicitly asks for it.
- Do not define implementation details that belong to engineering architecture.
- Do not over-document obvious rules; keep the output lean and high-signal.
- Do not force a full token model if the file only supports a smaller, partial foundation.
- Do not generate a guidelines output by default. The audit-only mode is the default.
- Do not write authoritative guidelines rules where the audit evidence is incomplete or unresolved.
- Do not use the guidelines output to turn this skill into a broad documentation generator. Only project rules directly derivable from the audit are in scope.
- If `Guidelines.md` is non-empty, never replace its content. Propose targeted additions or revisions only.

## Edge cases

- No variables exist, but reusable styles or components do exist.
  Normalize the smallest useful set first. Do not invent a large token taxonomy without evidence.

- Variables exist, but local overrides dominate usage.
  Treat this as a normalization problem. Prefer bringing repeated overrides back to semantic variables.

- Multiple libraries or duplicate components exist.
  Pick one canonical source for the current task if the evidence is clear. Otherwise flag the conflict explicitly.

- Naming is inconsistent across old and new assets.
  Avoid expanding the inconsistent pattern. Choose a simple naming rule for the scoped area first, then continue with only the minimum local or scoped creation needed to keep work coherent.

- Existing components are visually inconsistent but widely used.
  Prefer incremental correction through shared rules and extension, not broad replacement without scope.

- Accessibility issues conflict with legacy visual choices.
  Flag the issue. Use `references/accessibility.md` to classify whether the problem is contrast, color-only communication, touch target sizing, or responsive inconsistency. Accessibility basics should be treated as a system-level defect, not as a one-off exception.

- Responsive targets are unknown.
  Apply only basic responsive checks and label the breakpoint logic as unresolved. Do not invent a breakpoint strategy without evidence.

- `Guidelines.md` is empty.
  The skill may propose a conservative baseline if the audit produced enough resolved evidence. The baseline must separate active rules, holds, and unresolved decisions clearly. It must not read as a final or complete design system specification.

- `Guidelines.md` already exists and has content.
  Produce a targeted patch proposal only. Identify specific sections or rules that should be added, corrected, or flagged as outdated based on the current audit. Do not replace the file or rewrite sections that the audit did not review.

- The system is fully unresolved after the audit.
  Do not generate a guidelines output. Record the blocker in the open points and stop. A guidelines output on top of an unresolved system produces false certainty.

- Guidelines output is requested but the audit scope was narrow.
  Limit the guidelines output to the audited scope. Label clearly that the output covers only the reviewed area and does not represent the full system.

## Final checklist

### Audit checklist (always)

- Canonical library or local system source identified
- Reuse-first decision applied
- Variable and style usage reviewed
- Naming pattern checked or stabilized
- Component gaps identified
- States and variants reviewed at least for core patterns
- Repeated layout structures checked for consistent spacing and inferred auto layout behavior
- Contrast basics checked where semantic colors are in use
- Color-only state communication reviewed
- Touch target basics checked where touch interaction is expected
- Basic responsive assumptions checked or marked unresolved
- Basic accessibility checks completed
- Ambiguities and unresolved conflicts called out explicitly

### Guidelines output checklist (only when guidelines mode is active)

- Guidelines mode was explicitly requested or `Guidelines.md` is empty
- Audit was completed before guidelines output was generated
- Active project rules contain only audit-resolved items
- Holds list includes deferral reasons
- Unresolved decisions list is non-empty if the audit had open points
- No active rule was written for a system item that remains unresolved
- If `Guidelines.md` exists and is non-empty, a patch was proposed rather than a full replacement
- Output is scoped to the audited area; any wider claim is labeled as out of scope
- No fabricated certainty: every rule is traceable to an audit finding
