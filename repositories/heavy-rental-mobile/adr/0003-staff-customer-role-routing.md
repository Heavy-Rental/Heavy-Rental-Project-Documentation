# ADR 0003: Client-side staff vs customer routing

- Status: accepted
- Date: 2026-08-21

## Context
Spring issues role claims. A full in-app RBAC model is out of scope.

## Decision
Route after login using the access token `roles` claim. Customers get a read-only bookings screen.

## Consequences
No finer-grained permissions; server still enforces PATCH rules.
