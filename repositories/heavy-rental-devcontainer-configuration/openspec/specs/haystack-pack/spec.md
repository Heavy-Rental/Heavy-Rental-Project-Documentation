# haystack-pack Specification

## Purpose

The Haystack pack SHALL provide local Postgres+pgvector, pull-merge, Neo4j, and populate.

## Requirements

### Requirement: Skip on primary down
Default sync SHALL skip cycles when `postgres-primary` is unreachable and SHALL NOT wipe local data.

#### Scenario: Populate isolation
- **THEN** populate never drops KG-1 `:Document`
