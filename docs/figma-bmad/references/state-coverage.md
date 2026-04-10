# State Coverage

Review state coverage only for the scope being handed off.

## Common states to consider

- default
- loading
- empty
- error
- success
- disabled

## Decision rule

- If a state is critical to the scoped interaction and missing, readiness cannot be `ready`.
- If the state is likely relevant but not proven critical, mark `partial`.
- If the scope clearly does not require that state, its absence is acceptable.

## Warning

Do not assume a state is optional just because the default view looks complete.
