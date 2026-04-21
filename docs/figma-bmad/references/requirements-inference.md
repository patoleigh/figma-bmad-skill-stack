# Requirements Inference

Use this reference during `figma-bmad-mockup-to-requirements` to translate visible design evidence into conservative requirements inferences.

## Core principle: Conservative inference

Infer only what can be reasonably concluded from visible evidence. When evidence could support multiple interpretations, record the ambiguity rather than choosing arbitrarily.

## What can be inferred safely

### Screen purpose

From visible evidence, you can infer:

- **What the screen enables the user to do**: Based on primary controls and layout structure
- **What user goal the screen serves**: Based on heading, primary action, and content structure

Safe inference signals:

- A form with input fields and a "Submit" button → likely a creation or submission screen
- A list or table with search/filter controls → likely a discovery or browse screen
- A detail view with edit/delete actions → likely a management or detail screen
- A confirmation message or success indicator → likely a confirmation or result screen

Unsafe inference (do not do this):

- Inventing multi-step workflows from a single screen
- Assuming complex business logic not visible in the UI
- Fabricating user roles or permissions not shown

### User goal

From visible evidence, you can infer:

- **Why a user would arrive at this screen**: Based on heading, entry context, and primary action
- **What the user is trying to accomplish**: Based on the primary action and supporting controls

Safe inference signals:

- A heading "Login" with email/password inputs → user goal is to authenticate
- A heading "Checkout" with payment inputs → user goal is to complete a purchase
- A heading "Search Results" with a list → user goal is to find a specific item

Unsafe inference:

- Inventing user motivations not suggested by the UI
- Assuming user journey steps not shown in the mockup
- Fabricating user segmentation or role-based behavior

### Primary actions

From visible evidence, you can infer:

- **The main action the user can take**: Based on the most prominent button or control
- **What happens when the user takes the primary action**: Based on button label and form structure

Safe inference signals:

- A prominent "Submit" button on a form → primary action is to submit the form
- A prominent "Add to Cart" button on a product view → primary action is to add the product
- A prominent "Search" button next to a search input → primary action is to search

Unsafe inference:

- Fabricating multi-step actions from a single button
- Assuming backend processing not visible in the UI
- Inventing validation or business rules not shown

### Secondary actions

From visible evidence, you can infer:

- **Supporting actions the user can take**: Based on secondary buttons, links, or navigation
- **Optional or alternative paths**: Based on less prominent controls

Safe inference signals:

- A "Cancel" button next to a "Submit" button → secondary action is to cancel
- A "Save Draft" button next to a "Publish" button → secondary action is to save without publishing
- A "Back" link or breadcrumb → secondary action is to navigate back

Unsafe inference:

- Inventing actions not visible in the mockup
- Assuming navigation destinations not shown

### States and state transitions

From visible evidence, you can infer:

- **States shown in the mockup**: Directly observed
- **States likely required but not shown**: Based on primary action and control types

Safe inference signals:

- A submit button is shown → likely required states: default, loading, success, error
- A list is shown with items → likely required states: default (with items), empty (no items), loading
- An input field is shown → likely required states: default, focus, error (validation)

Unsafe inference:

- Inventing complex state machines not suggested by the UI
- Assuming state transitions without visible evidence
- Fabricating error states not hinted by the control types

### Business rules and validation

From visible evidence, you can infer:

- **Validation constraints hinted by input types**: Email inputs suggest email validation, password inputs suggest password constraints
- **Required fields**: Based on asterisks, "required" labels, or visual emphasis
- **Format constraints**: Based on placeholder text or input masks

Safe inference signals:

- An input with placeholder "name@example.com" → likely email format validation
- A password input with helper text "Must be 8+ characters" → likely password length constraint
- An input marked with an asterisk → likely required field

Unsafe inference:

- Fabricating detailed validation rules not shown
- Inventing business logic beyond what the UI hints
- Assuming backend validation without visible error messages

### Dependencies between UI elements

From visible evidence, you can infer:

- **Conditional visibility**: When controls appear to enable/disable based on other controls
- **Required sequences**: When the layout suggests a progression
- **Related inputs**: When inputs are visually grouped

Safe inference signals:

- A "Billing Address" section with a checkbox "Same as shipping address" → dependency between billing and shipping
- A dropdown "Country" followed by "State/Province" → state options likely depend on country
- A checkbox "I agree to terms" near a disabled "Submit" button → submit likely depends on agreement

Unsafe inference:

- Inventing data dependencies not suggested by the UI
- Fabricating complex conditional logic from simple grouping
- Assuming backend relationships without visible evidence

## Confidence levels for inference

### High confidence

Infer with high confidence when:

- The visible evidence strongly suggests a specific requirement
- Multiple visible signals support the same conclusion
- The inference is narrow and grounded in observable elements

Example: A form with "Email" and "Password" inputs and a "Log In" button → high confidence that the requirement is "user can log in with email and password."

### Medium confidence

Infer with medium confidence when:

- The visible evidence suggests a requirement but some details are unclear
- The inference requires one or two small assumptions
- The requirement is reasonably scoped but not fully specified

Example: A button labeled "Next" at the bottom of a form → medium confidence that there is a multi-step flow, but the number of steps and progression logic are unclear.

### Low confidence

Infer with low confidence when:

- The visible evidence is limited or ambiguous
- Multiple interpretations are possible
- The inference requires several assumptions

Example: A list with no visible search or filter controls → low confidence about whether search/filter is required, or whether the list is always short enough not to need it.

## When NOT to infer

Do not infer when:

- **The evidence is too limited**: If the mockup shows only a partial screen or section, do not infer requirements for the full feature.
- **Multiple interpretations are equally valid**: Record the ambiguity instead of choosing one.
- **The inference would require inventing product strategy**: Do not fabricate user segmentation, business models, or product vision.
- **The inference would require inventing backend behavior**: Do not fabricate API contracts, database schemas, or architecture.
- **The inference would be a guess**: If you find yourself saying "maybe" or "probably," record it as an assumption or open question instead.

## Separating inference from assumption

An **inference** is a conservative conclusion grounded in visible evidence.

An **assumption** is something you must assume to produce the inference, but cannot directly observe.

Example:

- **Visible evidence**: A search input and a "Search" button
- **Inference**: The primary action is to search
- **Assumption**: Searching queries a backend API (not visible in the mockup)
- **Assumption**: Search results are filtered by keyword (not shown in the mockup)

Always separate inferences from assumptions in the requirements draft.

## Requirements inference checklist

- [ ] Screen purpose inferred conservatively from visible controls and layout
- [ ] User goal inferred from heading, primary action, and content structure
- [ ] Primary actions identified based on prominent controls
- [ ] Secondary actions identified based on supporting controls
- [ ] Required states inferred based on control types and primary actions
- [ ] Business rules and validation inferred only from visible hints
- [ ] Dependencies inferred only from visible relationships
- [ ] Confidence level assessed for each inference
- [ ] No product strategy fabricated
- [ ] No backend behavior invented
- [ ] No guesses presented as inferences
- [ ] All assumptions separated from inferences
