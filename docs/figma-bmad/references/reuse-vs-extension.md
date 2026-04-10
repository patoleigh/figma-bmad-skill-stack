# Reuse vs Extension

## Reuse first

Reuse when:

- the component already matches the role
- the behavior is correct
- the existing states and variants are sufficient

## Extend when needed

Extend when:

- the pattern family is correct
- only a state, variant, or bounded adaptation is missing
- extending preserves system consistency better than creating new

## Escalate or block

Escalate or block when:

- the need is really a design-system gap
- no existing role-correct pattern exists
- solving the case would introduce a parallel component family
- the file contains conflicting canonical sources

## Anti-patterns

- creating a new component because an old one is inconvenient
- forcing a visually similar component into the wrong role
- solving a system gap as a local page exception
