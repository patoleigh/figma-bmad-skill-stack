# Figma BMAD Mockup to Requirements

## Purpose

Use this skill to infer a structured requirements draft from an existing Figma mockup, screen, or selection when the original product requirements are missing or were never documented.

The skill is intentionally narrow. Its job is to:

- analyze visible design evidence in an existing Figma mockup
- reconstruct likely product intent grounded in observable UI elements
- separate what is directly visible from what is reasonably inferred
- identify assumptions that should be validated
- surface missing requirement areas as open questions
- produce a compact requirements draft that can feed the rest of the stack

This skill produces a **requirements draft grounded in visible design evidence**, not a final PRD.

It is an auxiliary recovery tool for when requirements are missing, not a replacement for the default workflow of starting with real product requirements.

## Relationship to the stack

This skill is an **alternative entry point** when requirements are missing.

It is **not part of the mandatory default path**. The happy path still starts with real requirements.

### Position in the stack

This skill is **upstream of** and **feeds into**:

- `figma-bmad-prd-to-screen-plan`

It is **parallel to** (but does not replace):

- real product requirements documents
- PRDs, feature briefs, or product descriptions

It may **optionally consult**:

- `figma-bmad-design-system-rules` (to distinguish system conventions from product-specific intent)
- `Guidelines.md` (to avoid treating system-level patterns as product requirements)

### Workflow integration

**Recovery path** (when requirements are missing):
1. `figma-bmad-mockup-to-requirements` → produces `requirements/<feature-slug>-requirements-draft.md`
2. Validate the draft with product/design stakeholders
3. `figma-bmad-prd-to-screen-plan` → reads the validated requirements draft
4. `figma-bmad-compose-screen` → composes or updates the mockup
5. `figma-bmad-handoff-readiness` → evaluates readiness

**Happy path** (when requirements already exist):
1. (Real requirements) → `figma-bmad-prd-to-screen-plan` → `compose-screen` → `handoff-readiness`

This skill must not replace any other layer:

- If the task is to audit or normalize system rules, stop and defer to `figma-bmad-design-system-rules`.
- If the task is to plan views from known requirements, stop and defer to `figma-bmad-prd-to-screen-plan`.
- If the task is to compose screens, stop and defer to `figma-bmad-compose-screen`.

## When to use

Use this skill when the task is any of the following:

- a screen or mockup exists but requirements were never written down
- a team wants to recover product intent from legacy mockups
- a design needs to be reverse-documented before planning new work
- requirements need to be reconstructed before the rest of the stack can proceed
- a mockup exists and enough structure is needed to continue through the planning/composition/handoff workflow

Read references only as needed:

- `references/visual-evidence-extraction.md` for observing and cataloging visible design elements
- `references/requirements-inference.md` for conservative inference rules
- `references/assumptions-and-gaps.md` for separating evidence, inference, assumptions, and unknowns

## When NOT to use

Do not use this skill when the real task is:

- starting with known product requirements (use `figma-bmad-prd-to-screen-plan` directly)
- auditing or defining system rules inside the Figma file
- composing new screens or updating existing ones
- reviewing handoff readiness
- inventing product strategy where no design evidence exists
- creating a full PRD for an entire product from one view
- defining backend, API, or architecture contracts

If real product requirements already exist, use them directly. Do not run this skill to "validate" existing requirements by comparing them to mockups.

## Expected inputs

Required:

- a Figma file URL, node ID, or selection reference pointing to the mockup to analyze
- the existing Figma mockup, screen, or bounded selection to analyze

Optional but helpful:

- `Guidelines.md` from the project repo, to understand system-level conventions
- the system rule summary from `figma-bmad-design-system-rules`, to distinguish system patterns from product-specific intent
- any available product context: target user role, known constraints, business domain
- any partial requirements or known product decisions
- the feature area or product scope this mockup belongs to

## Expected outputs

This skill always produces two outputs:

1. **Chat output**: the compact requirements draft returned inline in the current session.
2. **Persistent artifact**: the same content written to `requirements/<feature-slug>-requirements-draft.md` in the project repo.

Both outputs use the same structure. The persistent artifact enables review, validation, and feed-forward into `prd-to-screen-plan`.

Content of the output:

- a compact requirements draft grounded in visible design evidence
- clear separation of observed evidence, inferred requirements, assumptions, and open questions
- likely screen purpose and user goal
- likely primary and secondary actions
- visible or implied states
- inferred business rules or validation constraints suggested by the UI
- dependencies between UI elements
- missing requirement areas that must be clarified

### Requirements artifact file path

Use the path: `requirements/<feature-slug>-requirements-draft.md`

Rules for the feature slug:

- Derive from the mockup's apparent feature area, screen name, or product scope
- Use kebab-case. Remove articles and stop words. Keep it short and scannable.
- Examples: `requirements/user-authentication-requirements-draft.md`, `requirements/checkout-flow-requirements-draft.md`, `requirements/dashboard-overview-requirements-draft.md`

Rules for update vs create:

- If `requirements/<feature-slug>-requirements-draft.md` already exists, open and update it instead of creating a new file.
- Do not create a second file for the same feature scope.
- If no requirements file exists for the current scope, create one.

Use this compact output shape so results stay consistent between runs:

```md
## Requirements draft summary

- Source: [Figma mockup reference or node ID]
- Feature scope: [overall product area or feature]
- Confidence: [high | medium | low]
- Evidence basis: [strong visible evidence | mixed visible evidence | limited visible evidence]

## Observed evidence

### Layout and structure
- [directly visible sections, hierarchy, grouping]

### UI elements and components
- [visible controls, inputs, buttons, navigation, feedback areas]

### Visible copy and labels
- [text content, headings, button labels, placeholders, error messages]

### Implied interactions
- [interactions suggested by control types: clickable, editable, selectable, draggable]

### Visible states
- [states shown in the mockup: default, loading, empty, error, success, disabled, selected]

## Inferred requirements

### Screen purpose
- [what this screen likely enables the user to do, inferred from visible evidence]

### User goal
- [likely user intent when arriving at this screen]

### Primary actions
- [main actions the user can take, inferred from prominent controls]

### Secondary actions
- [supporting actions or navigation options]

### States and state transitions
- [states not shown but likely required, based on primary actions]

### Business rules
- [validation, constraints, or business logic hinted by the UI]

### Dependencies
- [implied relationships between UI elements or data dependencies]

## Assumptions made

- [explicit list of assumptions required to produce the inferred requirements]
- [each assumption should be marked for validation]

## Missing requirements / open questions

- [requirement areas that cannot be inferred from visible evidence]
- [product decisions that must be answered before requirements can be finalized]
- [ambiguities where multiple interpretations are possible]
```

## Core workflow

1. Read project guidelines if available.
   Check whether `Guidelines.md` exists in the project repo. If it does, read it to understand system-level conventions. Use this to distinguish generic design-system patterns from product-specific intent. If `Guidelines.md` does not exist, proceed without it and note the absence.

2. Optionally consult the system rule summary.
   If a system rule summary from `figma-bmad-design-system-rules` is available in the current session, review it to understand which patterns are system-level versus product-specific. This is optional but helpful.

3. Confirm the mockup scope.
   Identify the specific Figma mockup, screen, or selection being analyzed. Establish the apparent feature area or product scope. Do not analyze beyond the visible mockup.

4. Extract visible evidence.
   Use `references/visual-evidence-extraction.md` to systematically observe:
   - layout and structure: sections, hierarchy, grouping, spacing patterns
   - UI elements and components: controls, inputs, buttons, navigation, feedback areas
   - visible copy and labels: headings, button text, placeholders, error messages
   - implied interactions: what control types suggest (clickable, editable, selectable)
   - visible states: what states are shown in the mockup (default, loading, empty, error, success, disabled, selected)

5. Infer requirements conservatively.
   Use `references/requirements-inference.md` to translate visible evidence into requirements:
   - screen purpose: what this screen likely enables the user to do
   - user goal: why a user would arrive at this screen
   - primary actions: main actions inferred from prominent controls
   - secondary actions: supporting actions or navigation
   - required states: states not shown but likely necessary based on primary actions
   - business rules: validation, constraints, or logic hinted by the UI
   - dependencies: implied relationships between elements

6. Distinguish product requirements from system conventions.
   If guidelines or system rules are available, use them to avoid treating generic design-system patterns as product requirements. For example:
   - a standard button style is a system convention, not a product requirement
   - a specific validation message is a product requirement
   - a consistent spacing pattern is a system convention
   - a specific workflow implied by button placement is a product requirement

7. Separate evidence, inference, and assumptions.
   Use `references/assumptions-and-gaps.md` to structure the output:
   - **Observed evidence**: what is directly visible in the mockup
   - **Inferred requirements**: what can be reasonably concluded from the evidence
   - **Assumptions**: what must be assumed to produce the inferred requirements
   - **Open questions**: what cannot be inferred and must be answered by product/design

8. Identify missing requirement areas.
   For each inferred requirement, identify what is still unknown:
   - edge cases not shown in the mockup
   - business logic not visible in the UI
   - user role or permission requirements
   - data sources or backend behavior
   - cross-screen workflows or navigation logic
   - validation rules not obvious from control types

9. Assess confidence and evidence basis.
   Label the requirements draft with:
   - **Confidence**: how much of the feature scope is covered by the visible mockup (high | medium | low)
   - **Evidence basis**: how strong the visible evidence is (strong | mixed | limited)

10. Produce the compact requirements draft and write the artifact.
    Assemble the final output using the structure defined in `Expected outputs`. Keep it focused on what can be grounded in visible evidence.
    - Write or update the requirements artifact at `requirements/<feature-slug>-requirements-draft.md`.
    - If the file already exists, update it in place. Do not create a duplicate.
    - Also return the same content in chat as the session output.

## Decision rules

- Infer conservatively. When visible evidence could support multiple interpretations, record the ambiguity instead of choosing arbitrarily.
- Separate observed evidence from inferred requirements explicitly. The requirements draft must make clear what is directly visible versus reasonably concluded.
- Treat assumptions as provisional. Every assumption should be marked for validation.
- Prefer open questions to false certainty. If a requirement cannot be inferred from visible evidence, record it as an open question.
- Distinguish product requirements from system conventions. Generic design-system patterns are not product requirements.
- Avoid inventing deep business logic. If the UI hints at validation or constraints, note them, but do not fabricate detailed business rules.
- Do not invent backend or API contracts. The requirements draft should focus on user-facing behavior visible in the mockup.
- Keep the scope bounded. Only analyze the visible mockup. Do not invent requirements for screens or flows not shown.
- Confidence reflects evidence quality. Low confidence does not mean the draft is wrong — it means the mockup provides limited evidence.
- Assess evidence basis explicitly. Strong visible evidence supports confident inference; limited evidence requires more validation.

Requirements artifact rules:

- The requirements artifact is always written. It is not optional.
- Derive the feature slug from the mockup's feature area or screen name, in kebab-case.
- If the file `requirements/<feature-slug>-requirements-draft.md` already exists, update it. Do not create a duplicate.
- The content of the artifact must match the chat output exactly. There is one version, not two.

## Constraints

- Stay grounded in visible design evidence. Do not invent requirements beyond what the mockup shows or reasonably implies.
- Do not fabricate product strategy or deep business logic with false certainty.
- Do not generate a full PRD for an entire product if only one view is shown.
- Do not compose new screens or redefine system rules. The output is a requirements draft only.
- Do not perform handoff readiness evaluation. The output feeds planning, not implementation.
- Do not invent backend, API, or architecture contracts. Focus on user-facing behavior.
- Do not replace real product conversations. The requirements draft is a starting point for validation, not a final specification.
- Keep the output structure compact. A requirements draft that is too detailed to validate is not useful.
- Always write the requirements artifact. Skipping the file write is not permitted.
- Do not create a second requirements file for a scope that already has one. Update the existing file.

## Edge cases

- The mockup shows a complete screen with clear primary actions.
  Infer requirements with higher confidence. Still separate observed evidence from inferred requirements, and still list assumptions.

- The mockup shows only a partial screen or isolated section.
  Limit the requirements draft to the visible scope. Note explicitly that the draft covers only the visible area, not the full feature.

- The mockup shows multiple states (default, loading, error, success).
  Catalog all visible states in the observed evidence section. Infer requirements for state transitions based on the control types and visible state coverage.

- The mockup shows no error or edge-case states.
  Infer likely required states based on the primary actions, but list them as assumptions. Note the missing states as open questions.

- The mockup is visually polished but contains no copy or labels.
  Limit inferred requirements to structure and interaction patterns. Mark all copy-dependent requirements (validation messages, labels, headings) as open questions.

- The mockup uses generic placeholder content ("Lorem ipsum", "User Name", "Item 1").
  Treat placeholder content as evidence of structure only, not as product requirements. Note that real content requirements are missing.

- The mockup conflicts with known system conventions from `Guidelines.md`.
  Note the conflict explicitly. Do not treat the conflict as a product requirement without validation. Record it as an open question.

- Multiple mockups exist for the same feature scope.
  Analyze all available mockups together if they belong to the same bounded scope. If they show different states or flows, consolidate observed evidence and note any contradictions as open questions.

- The mockup implies a workflow or multi-step flow.
  Infer the likely flow steps from visible navigation or state progression. List the inferred flow in the requirements draft, but mark flow logic as an assumption requiring validation.

- The visible evidence is too limited to infer confident requirements.
  Produce a low-confidence draft. Label the evidence basis as "limited visible evidence." Do not inflate confidence by inventing requirements beyond what the mockup shows.

- `Guidelines.md` does not exist.
  Proceed without system-level context. Note in the requirements draft that system conventions were not consulted, which may affect the separation of product requirements from system patterns.

- A requirements artifact already exists for this feature scope.
  Read the existing file before starting. Update it in place based on the current mockup analysis. Do not create a parallel file. Preserve unchanged sections and update only what the current analysis changes.

## Final checklist

- `Guidelines.md` was read if it exists in the project repo, or the absence was noted
- System rule summary was consulted if available in the session, or the absence was noted
- Mockup scope is explicitly stated
- All visible evidence was cataloged systematically
- Observed evidence section contains only directly visible elements, not inferred requirements
- Inferred requirements section separates conservative conclusions from observed evidence
- Assumptions section explicitly lists all assumptions made
- Missing requirements / open questions section identifies what cannot be inferred
- Product requirements are distinguished from system conventions
- Deep business logic was not fabricated
- Backend, API, and architecture contracts were not invented
- Confidence and evidence basis are explicitly stated
- The requirements draft is compact enough to be validated with stakeholders
- Requirements artifact written to `requirements/<feature-slug>-requirements-draft.md` (created or updated)
- Chat output matches the artifact content exactly
