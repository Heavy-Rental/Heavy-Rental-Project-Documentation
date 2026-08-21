# ADR 0004: Resilience4j Haystack client

- Status: accepted
- Date: 2026-08-21

## Decision
Typed RestClient with timeouts, retry (ingest retry off by default), circuit breaker, and bulkheads. Map failures to recommender_* error codes.

## Consequences
Portal gets 502/503/504 instead of hanging. CRUD is independent of Haystack health.
