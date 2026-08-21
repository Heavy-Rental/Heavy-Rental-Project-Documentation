# fleet-mirror Specification

## Purpose

Haystack SHALL read fleet from local `postgres-haystack`, populated by pull-merge from Spring primary.

## Requirements

### Requirement: Pull only
The Haystack stack SHALL NOT write `postgres-primary`. Default sync SHALL skip when primary is down.

#### Scenario: Hostname
- **THEN** live compose uses `POSTGRES_HOSTNAME=postgres-haystack`, not `db`
