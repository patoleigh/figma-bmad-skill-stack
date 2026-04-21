# Assumptions and Gaps

Use this reference during `figma-bmad-mockup-to-requirements` to distinguish evidence, inference, assumptions, and open questions in the requirements draft.

## The four categories

A well-structured requirements draft separates:

1. **Observed evidence**: what is directly visible in the mockup
2. **Inferred requirements**: what can be reasonably concluded from the evidence
3. **Assumptions**: what must be assumed to produce the inferred requirements
4. **Open questions**: what cannot be inferred and must be answered by product/design

Mixing these categories produces false certainty and undermines the draft's value.

## Observed evidence

**Definition**: Anything directly visible in the mockup without interpretation.

**Examples**:
- "A button labeled 'Submit' is present"
- "Three input fields: Email, Password, and Confirm Password"
- "A heading reads 'Create Account'"
- "An error message is shown: 'Email is required'"

**Not evidence**:
- "The form validates email format" (inferred, not directly visible unless an error message is shown)
- "Clicking Submit sends data to the backend" (assumed, not visible)
- "The user must agree to terms" (inferred from a checkbox, not directly stated unless there is visible copy)

## Inferred requirements

**Definition**: Conservative conclusions grounded in visible evidence.

**Examples**:
- **Evidence**: A form with Email, Password, and a "Log In" button
- **Inference**: The primary action is to log in with email and password

- **Evidence**: A list with a search input and "Search" button
- **Inference**: The primary action is to search the list

- **Evidence**: A "Cancel" button next to a "Submit" button
- **Inference**: A secondary action is to cancel the operation

**Confidence markers**:
- High confidence: "The primary action is to submit the form" (strong evidence)
- Medium confidence: "The screen likely supports multi-step progression" (moderate evidence)
- Low confidence: "Search may support advanced filters" (weak evidence)

## Assumptions

**Definition**: Things you must assume to produce the inferred requirements, but cannot directly observe.

**Examples**:

- **Inferred requirement**: The primary action is to search
- **Assumption**: Search queries a backend API
- **Assumption**: Search results are filtered by keyword

- **Inferred requirement**: The user can log in with email and password
- **Assumption**: Credentials are validated against a user database
- **Assumption**: Invalid credentials produce an error message

- **Inferred requirement**: The form validates email format
- **Assumption**: Validation happens on the client side
- **Assumption**: Invalid email format blocks submission

**How to write assumptions**:
- State them explicitly: "Assumes that search queries a backend API"
- Mark them for validation: "Assumption: credentials are validated server-side (not shown in mockup)"
- Do not present them as requirements: Wrong: "The system validates credentials server-side" / Right: "Assumes credentials are validated (validation logic not visible)"

## Open questions

**Definition**: Requirement areas that cannot be inferred from visible evidence and must be answered by product/design.

**Examples**:

- **Evidence gap**: The mockup shows a default state but no error state
- **Open question**: What happens if login fails? What error message is shown?

- **Evidence gap**: The mockup shows a search input but no results
- **Open question**: How are search results displayed? What if there are no results?

- **Evidence gap**: The mockup shows a single screen but no navigation
- **Open question**: How does the user navigate to this screen? Where do they go after completing the action?

- **Ambiguity**: A button labeled "Next"
- **Open question**: Does "Next" mean next step in a flow, or next page of results?

**Types of open questions**:

### 1. Missing states
- The mockup shows default state but not loading, error, empty, or success states
- Questions: What does each state look like? What triggers state transitions?

### 2. Missing workflows
- The mockup shows a single screen but not the full flow
- Questions: What are the previous/next steps? How does the user navigate between them?

### 3. Missing validation or business rules
- The mockup hints at validation but does not show rules or error messages
- Questions: What are the exact validation rules? What error messages are shown?

### 4. Missing edge cases
- The mockup shows a happy path but not edge cases
- Questions: What happens if data is missing? What if the operation fails?

### 5. Ambiguous intent
- The mockup could support multiple interpretations
- Questions: Which interpretation is correct? What is the intended user goal?

### 6. Missing backend behavior
- The mockup shows UI but not backend logic
- Questions: What backend operations are triggered? What data is persisted?

### 7. Missing permissions or roles
- The mockup does not show user roles or permissions
- Questions: Who can access this screen? Are there role-based restrictions?

## How to structure the draft

Use this hierarchy to keep the categories clear:

```md
## Observed evidence

### Layout and structure
- [directly visible elements]

### UI elements and components
- [visible controls]

### Visible copy and labels
- [text content]

### Implied interactions
- [interactions suggested by control types]

### Visible states
- [states shown in the mockup]

## Inferred requirements

### Screen purpose
- [what this screen likely does, with confidence level]

### User goal
- [likely user intent, with confidence level]

### Primary actions
- [main actions, with confidence level]

### Secondary actions
- [supporting actions, with confidence level]

### States and state transitions
- [states not shown but likely required, with confidence level]

### Business rules
- [validation or constraints hinted by the UI, with confidence level]

### Dependencies
- [implied relationships, with confidence level]

## Assumptions made

- Assumption 1: [explicit assumption required for inference]
- Assumption 2: [mark for validation]
- ...

## Missing requirements / open questions

- Open question 1: [question that must be answered]
- Open question 2: [ambiguity that must be resolved]
- ...
```

## Decision rules for categorization

**When in doubt**:

- If it is directly visible → **Observed evidence**
- If it can be reasonably concluded from what is visible → **Inferred requirements**
- If you must assume it to produce an inference → **Assumptions**
- If you cannot infer it from visible evidence → **Open questions**

**Red flags for miscategorization**:

- Using "probably", "maybe", or "likely" in observed evidence → Move to inferred requirements or assumptions
- Stating backend behavior as an inferred requirement → Move to assumptions
- Inventing product strategy as an inferred requirement → Move to open questions
- Mixing observed evidence with interpretation → Separate into evidence and inference

## Validation strategy

A well-structured requirements draft enables efficient validation:

1. **Observed evidence**: Stakeholders confirm "yes, that is what the mockup shows"
2. **Inferred requirements**: Stakeholders confirm "yes, that is the intended behavior" or correct misinterpretations
3. **Assumptions**: Stakeholders confirm or correct each assumption
4. **Open questions**: Stakeholders provide answers

If the draft mixes these categories, validation becomes ambiguous: stakeholders cannot tell what is being claimed versus what is being asked.

## Checklist for assumptions and gaps

- [ ] Observed evidence contains only directly visible elements
- [ ] Inferred requirements are conservative and grounded in evidence
- [ ] Every inference is supported by visible evidence
- [ ] Assumptions are explicitly listed and separated from requirements
- [ ] Each assumption is marked for validation
- [ ] Open questions identify missing requirement areas
- [ ] No backend behavior is stated as a requirement without qualification
- [ ] No product strategy is fabricated as a requirement
- [ ] Confidence levels are stated where relevant
- [ ] The draft structure clearly separates the four categories
