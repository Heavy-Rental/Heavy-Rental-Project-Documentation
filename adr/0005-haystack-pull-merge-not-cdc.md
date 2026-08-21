# ADR 0005: Haystack fleet mirror is pull-merge, not CDC

- Status: accepted
- Date: 2026-08-21
- Related: devcontainer ADR-0003, ADR-0004

## Context

Logical replication / CDC is operationally heavy for a student Academy lab and local Compose.

## Decision

`postgres-haystack-sync` polls the primary (~60s), upserts an allowlist, and skips when the primary is down. It does not push from Spring and does not install pgvector on the primary.

## Consequences

- Near-real-time, not strictly real-time.
- Local AI work survives primary downtime.
