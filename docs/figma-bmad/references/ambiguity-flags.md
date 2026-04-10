# Ambiguity Flags

Flag ambiguity only when it can materially confuse implementation.

## Common ambiguity flags

- unclear primary action
- unclear hierarchy between sections
- two competing component patterns for the same role
- unclear variant or state selection
- naming that does not reveal purpose
- local exception that conflicts with the canonical source
- visible interaction with no clear success, error, or empty behavior

## Escalation rule

If the ambiguity belongs to system rules or composition, do not solve it here. Mark it and downgrade readiness.
