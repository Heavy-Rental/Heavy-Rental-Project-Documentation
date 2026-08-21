# ADR 0001: Interim JWT then access JWT

- Status: accepted
- Date: 2026-08-21

## Decision
Public mint of a short-lived interim token; login consumes it and issues an access token with DB roles. Denylist `jti` on login (interim) and logout (access).

## Consequences
Clients must perform two calls. Login cannot be called with an access token.
