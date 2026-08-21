# ADR 0001: Internal-only HTTP

- Status: accepted
- Date: 2026-08-21

## Decision
Haystack binds internal `/internal/v1/...` routes. Spring is the only product caller.

## Consequences
No JWT on Haystack; network isolation and Spring auth are the controls.
