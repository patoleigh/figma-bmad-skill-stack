# Accessibility and Responsive Basics

## Accessibility basics

- Check contrast on semantic color choices and common text usage.
- Do not rely on color alone to communicate state.
- Make sure interactive patterns can remain understandable across their states.
- Treat accessibility basics as system rules, not as optional polish.

## Touch targets

- Where touch interaction is expected, keep target sizing usable and consistent.
- BMAD source material explicitly points to minimum `44x44px` touch targets in responsive/accessibility guidance.

## State clarity

- Disabled, error, success, and loading states should remain distinguishable without guesswork.
- Feedback patterns should be consistent across the system.

## Responsive basics

- If breakpoints are known, check that the system supports them consistently.
- If breakpoints are unknown, do only basic checks and mark the breakpoint strategy unresolved.
- Repeated layout structures should adapt consistently, not be manually redrawn in unrelated ways.

## Figma translation note

- BMAD source material speaks in terms of responsive strategy, breakpoints, layout, and accessibility.
- Translating that to Figma, review the system at the pattern level: container behavior, spacing changes, visible hierarchy, and touch-friendly interaction areas.

## Anti-patterns

- Color-only status changes
- Touch targets that work on desktop but collapse on mobile
- Responsive behavior handled as one-off exceptions instead of system rules
- Legacy visual decisions kept without flagging accessibility conflicts
