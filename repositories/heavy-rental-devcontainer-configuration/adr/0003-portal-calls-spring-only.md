# ADR 0003: Portal calls Spring only

- Status: accepted
- Date: 2026-08-21

## Decision
Portal pack has no DB and no Haystack client. Recommend is Spring dual-hop.

## Consequences
UI + CRUD work without Haystack; assistant needs both Spring and Haystack.
