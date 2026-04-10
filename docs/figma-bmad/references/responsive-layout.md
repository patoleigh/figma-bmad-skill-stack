# Responsive Layout

## Composition-level checks

- Keep repeated layouts structurally consistent across similar screens.
- Reuse the same spacing and container logic where the pattern repeats.
- Do not introduce one-off responsive behavior for a local fix if the rest of the file handles similar cases differently.

## When breakpoints are known

- Check that the composed area follows the expected layout adaptation.
- Keep hierarchy, action placement, and feedback zones understandable after layout changes.

## When breakpoints are unknown

- Apply only basic responsive checks.
- Mark breakpoint logic as unresolved instead of inventing a new rule.

## Touch and readability basics

- Where touch interaction is expected, keep touch target basics in mind.
- Avoid layout collapse that makes states or actions unclear.

## Anti-patterns

- one-off layout exceptions that break the current file's pattern
- responsive behavior solved visually but not structurally
- losing the primary action when the layout compresses
