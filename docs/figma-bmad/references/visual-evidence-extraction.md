# Visual Evidence Extraction

Use this reference during `figma-bmad-mockup-to-requirements` to systematically observe and catalog visible design elements in an existing mockup.

## What counts as visual evidence

Visual evidence is anything directly observable in the mockup without interpretation or inference. Evidence includes:

- layout and structure
- UI elements and controls
- visible copy and labels
- visible states
- implied interactions based on control types

Visual evidence does **not** include:

- inferred business logic
- assumed validation rules not visible in the UI
- hypothetical edge cases not shown
- backend behavior or data sources
- workflows not shown in the mockup

## How to extract evidence systematically

### 1. Layout and structure

Observe and catalog:

- **Sections and hierarchy**: How is the screen divided? Are there clear header, body, sidebar, or footer areas?
- **Grouping and containers**: What visual grouping exists? Are there cards, panels, or other bounded areas?
- **Spacing and density**: What spacing patterns are visible? Is the layout dense or spacious?
- **Alignment and grid**: How are elements aligned? Is there a visible grid structure?

Record only what is visible. Do not infer responsive behavior or breakpoint logic unless multiple layouts are shown.

### 2. UI elements and components

Observe and catalog:

- **Buttons**: What buttons are present? What do they say? What emphasis level (primary, secondary, tertiary)?
- **Inputs and forms**: What input fields exist? What types (text, number, date, dropdown, checkbox, radio)?
- **Navigation**: What navigation elements are visible? Tabs, breadcrumbs, links, back buttons?
- **Feedback areas**: Where would success, error, or loading feedback appear? Are any feedback states shown?
- **Lists and tables**: What data structures are visible? Lists, tables, grids, cards?
- **Media**: Are there images, icons, avatars, or other media elements?

Record the presence and type of controls. Defer interaction inference to the next step.

### 3. Visible copy and labels

Observe and catalog:

- **Headings and titles**: What are the main headings? What hierarchy (H1, H2, H3)?
- **Button labels**: What do buttons say? ("Submit", "Cancel", "Next", "Save Draft")?
- **Input labels and placeholders**: What are inputs labeled? What placeholder text exists?
- **Error or validation messages**: Are any error messages visible? What do they say?
- **Help text or hints**: Is there instructional or supporting text?
- **Empty state messages**: If an empty state is shown, what does it say?
- **Link text**: What link labels exist?

Record actual copy when present. Note when placeholder content like "Lorem ipsum" or "User Name" is used — this is evidence of structure, not content requirements.

### 4. Implied interactions

Based on visible control types, catalog what interactions are implied:

- **Clickable**: Buttons, links, tabs imply click actions
- **Editable**: Text inputs, dropdowns, checkboxes imply edit actions
- **Selectable**: Radio buttons, checkboxes, list items imply selection
- **Draggable**: Handles, reorder indicators imply drag actions
- **Navigable**: Breadcrumbs, tabs, links imply navigation
- **Submittable**: Forms with a submit button imply a submit action

This is still evidence-based observation. You are noting what control types suggest, not inventing workflows.

### 5. Visible states

Observe and catalog what states are shown in the mockup:

- **Default state**: The standard appearance
- **Loading state**: Spinners, skeletons, or loading indicators
- **Empty state**: "No results", "No items yet", or empty list messages
- **Error state**: Error messages, error styling, validation feedback
- **Success state**: Success messages, confirmation indicators
- **Disabled state**: Disabled buttons, read-only inputs
- **Selected state**: Selected items, active tabs, checked checkboxes
- **Focus state**: Focus indicators on inputs or controls

Only catalog states that are **directly visible** in the mockup. Do not infer states that are not shown.

## What NOT to extract as evidence

### Do not extract:

- **Inferred business logic**: If the mockup shows a "Submit" button, the evidence is "a submit button exists." Do not extract "the form validates inputs before submission" unless validation messages are visible.
- **Assumed workflows**: If the mockup shows a single screen, do not extract multi-step workflows unless navigation between steps is visible.
- **Backend behavior**: If the mockup shows a search input, the evidence is "a search input exists." Do not extract "search queries the backend API" or "search filters by keyword."
- **Data sources**: If the mockup shows a list of items, the evidence is "a list structure with N items." Do not extract "data is fetched from the database."
- **Edge cases not shown**: If the mockup shows only a default state, do not extract "handles network errors gracefully" as evidence.
- **Responsive behavior**: Unless multiple breakpoints or layouts are shown, do not extract responsive behavior as evidence.

## Cataloging placeholder vs real content

When the mockup uses placeholder content:

- **Generic placeholders** ("Lorem ipsum", "User Name", "Item 1"): Evidence of structure only. Do not treat as content requirements.
- **Realistic placeholders** ("john.doe@example.com", "Product Title"): Weak evidence of content type. Note the pattern, but mark content requirements as assumptions.
- **Real copy** (actual error messages, specific labels): Strong evidence. Catalog as observed copy.

## Handling ambiguous evidence

When evidence could support multiple interpretations:

- Catalog what is directly visible
- Note the ambiguity in the extraction
- Defer interpretation to the inference step

Example:
- **Visible**: A button labeled "Next"
- **Ambiguous**: Does "Next" mean "next step in a flow" or "next page of results"?
- **Catalog**: "Button labeled 'Next' is present"
- **Defer**: Record the ambiguity; infer intent during requirements inference

## Evidence extraction checklist

- [ ] Layout sections and hierarchy cataloged
- [ ] UI elements and controls cataloged by type
- [ ] Visible copy and labels recorded
- [ ] Implied interactions cataloged based on control types
- [ ] Visible states cataloged (only what is shown in the mockup)
- [ ] Placeholder content distinguished from real content
- [ ] Ambiguous evidence noted for later interpretation
- [ ] No inferred business logic included as evidence
- [ ] No assumed workflows included as evidence
- [ ] No backend behavior included as evidence
