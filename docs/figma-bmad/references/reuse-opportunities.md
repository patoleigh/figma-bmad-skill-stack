# Reuse Opportunities

Use this reference during `figma-bmad-prd-to-screen-plan` to identify likely reuse opportunities from the current system before composition begins.

## Purpose of pre-composition reuse identification

At the planning stage, reuse identification is directional, not prescriptive. The goal is to flag which pattern families and system areas are likely relevant for each view, so that composition can start from the right place instead of from scratch.

This reference is different from `references/reuse-vs-extension.md`, which is used during composition to make specific reuse or extension decisions. This reference guides which areas of the system to look at *before* composition begins.

## Pattern families to consider

When reviewing views in the screen plan, consider which of the following pattern families from the current system are likely relevant:

### Navigation patterns
- primary navigation structure (nav bar, sidebar, tab bar)
- back/forward or breadcrumb navigation
- modal or overlay navigation

Flag as a reuse opportunity when: the view requires a navigational container or entry/exit point.

### List and collection patterns
- item lists, card grids, data tables
- sorted, filtered, or grouped collection displays
- search and filtering patterns

Flag as a reuse opportunity when: the view displays a collection of items or allows discovery.

### Form and input patterns
- input fields, dropdowns, toggles, date pickers
- multi-step or sectioned forms
- inline editing

Flag as a reuse opportunity when: the view involves user data entry or configuration.

### Feedback and status patterns
- inline validation and error messages
- toast or snackbar notifications
- success and confirmation states
- empty states

Flag as a reuse opportunity when: the view has a primary action that produces a visible outcome or may fail.

### Loading patterns
- skeleton screens, spinners, progress indicators

Flag as a reuse opportunity when: the view retrieves data asynchronously.

### Detail and content patterns
- detail panels, content cards, expanded item views
- media or asset display areas

Flag as a reuse opportunity when: the view displays rich detail for a single item.

### Action and control patterns
- primary and secondary buttons
- action menus, dropdowns, or overflow controls
- confirmation dialogs

Flag as a reuse opportunity when: the view has explicit user actions.

## Cross-view reuse opportunities

Some pattern families recur across multiple views in a plan. These are especially worth flagging because consistent use is more valuable than per-view composition decisions. Common cross-view patterns:

- navigation structure shared across all views
- feedback patterns used wherever the user performs an action
- empty states used in every collection view
- loading patterns used wherever data is fetched

## Working approach

1. For each view in the plan, review the primary action and critical states.
2. Match those against the pattern family list above.
3. Note which pattern families are likely relevant — without naming specific components or variants.
4. Review the set of views as a whole and flag any pattern families that appear across multiple views.
5. If a pattern family is required but absent from the current system, flag it as a pre-composition blocker, not a reuse opportunity.

## Anti-patterns

- Pre-selecting specific components or variants at the planning stage — that belongs to composition
- Assuming reuse is possible without checking whether the pattern family exists in the current system
- Marking every pattern family as a potential reuse opportunity without discrimination
- Treating a missing pattern family as a reuse opportunity — absence is a blocker, not a starting point
