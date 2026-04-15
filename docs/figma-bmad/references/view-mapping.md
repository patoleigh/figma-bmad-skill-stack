# View Mapping

Use this reference during `figma-bmad-prd-to-screen-plan` to translate product requirement language into bounded view definitions.

## What a view is

A view is a bounded UI area that enables the user to perform a specific purpose or complete a step in a flow. A view is defined by what it does for the user, not by its visual structure or page layout.

Views are not:
- layout regions of a single screen (header, sidebar, footer)
- technical states of the same UI area
- variations of the same purpose for different user roles

## How to extract views from requirements

### Look for user purposes

Each distinct thing a user needs to accomplish is a candidate for a separate view. Common signals:

- "a user can view/browse/search [something]" → likely a list or discovery view
- "a user can create/add/submit [something]" → likely a creation or form view
- "a user can review/manage/edit [something]" → likely a detail or management view
- "a user receives confirmation/feedback" → may be a dedicated state or a lightweight confirmation view
- "a user must authenticate/onboard/set up" → likely a distinct entry flow view

### Look for flow steps

If requirements describe a user journey with clear steps, each step is a candidate for a distinct view. Flow-step signals:

- requirements that reference "before/after" relationships
- requirements that describe what a user sees "next" or "then"
- requirements that describe distinct success or error paths

### When to merge views

Merge candidate views when:

- they serve the same user purpose in the same flow step
- they differ only in content density, not in user action
- one is a simple modal or overlay of another with a clear scope boundary

Do not merge views when:

- they represent fundamentally different user actions
- they would force composition to handle incompatible state sets
- requirements treat them as separate named areas

### When to split views

Split candidate views when:

- a single view description implies two different primary user actions
- two user roles see meaningfully different content in the same "screen"
- the requirements explicitly separate two concerns that appear in the same surface

## Naming views

- Use purpose-based names, not layout-based names
- Prefer: `Dashboard`, `Order Detail`, `Product Search`, `Checkout`, `Empty State`
- Avoid: `Main Page`, `Top Section`, `Content Area`, `Screen 3`
- Keep names short and stable — they will be referenced across planning and composition runs

## Anti-patterns

- Mapping technical features directly to views ("API response view")
- Treating every state (empty, error, success) as a separate view
- Creating views for pure navigation or structural elements with no user purpose
- Over-splitting views for every minor content variation
- Under-splitting views by forcing multiple unrelated user actions into one scope
