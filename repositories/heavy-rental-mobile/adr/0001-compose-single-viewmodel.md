# ADR 0001: Jetpack Compose + single AppViewModel

- Status: accepted
- Date: 2026-08-21

## Context
v1 has a small screen set (login, home, deliveries, returns, customer bookings).

## Decision
Use Jetpack Compose and one `AppViewModel` owning auth, lists, and transitions.

## Consequences
Simple demo; will need splitting if screens grow.
