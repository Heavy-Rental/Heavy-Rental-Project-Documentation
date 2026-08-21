# ADR 0004: Spring PostgreSQL primary is the OLTP source of truth

- Status: accepted
- Date: 2026-08-21
- Related: devcontainer ADR-0002

## Context

Haystack needs fleet rows for ranking without sharing the OLTP extension surface (pgvector).

## Decision

Spring `postgres-primary` (`heavy_rental`) is the only product writer. Haystack uses a separate Postgres. Fix booking/fleet bugs in Spring, not by editing the mirror.

## Consequences

- Clear write authority.
- Mirror lag (~60s) is acceptable for recommend LTM.
