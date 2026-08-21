# rest-pack Specification

## Purpose

Operators SHALL choose with-replica or without-replica and promote `.devcontainer` to `Heavy-Rental-REST-API/`.

## Requirements

### Requirement: App always on primary
JDBC SHALL target `db-primary:5432`. Replica (if present) is read-experiment only.

#### Scenario: Ports
- **THEN** host 8080 app, 5432 primary, 5433 replica when selected
