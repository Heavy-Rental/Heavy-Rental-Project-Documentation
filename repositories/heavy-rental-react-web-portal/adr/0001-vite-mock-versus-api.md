# ADR 0001: Vite mock vs API modes

- Status: accepted
- Date: 2026-08-21

## Decision
Ship `dev:mock` (port 4010) and `dev:api` (Spring 8080) so UI can proceed without a backend.

## Consequences
Two env files; mock logins must not be confused with Spring seed users.
