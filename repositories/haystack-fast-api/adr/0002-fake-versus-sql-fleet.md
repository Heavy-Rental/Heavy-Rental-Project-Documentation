# ADR 0002: Fake vs SQL fleet backends

- Status: accepted
- Date: 2026-08-21

## Decision
`FLEET_BACKEND=fake` for tests/smoke; `sql` for live `assets.id` quotes.

## Consequences
Call 2 identity differs by profile; docs must not mix AST-* with live PK.
