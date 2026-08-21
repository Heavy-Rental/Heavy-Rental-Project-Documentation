# ADR 0003: Portal and mobile call Spring REST only

- Status: accepted
- Date: 2026-08-21
- Related: heavy-rental-devcontainer-configuration ADR-0006

## Context

Haystack and Stripe have internal or secret surfaces. Exposing them to the browser would duplicate auth and leak keys.

## Decision

The React portal and Android app SHALL use Spring REST as the only product HTTP backend. Spring dual-hops to Haystack. Stripe secrets stay on the server; the portal uses `clientSecret` from `deposit-intent`.

## Consequences

- Single public API, JWT, and error shape.
- Recommend fails closed when Haystack is down; CRUD still works.
