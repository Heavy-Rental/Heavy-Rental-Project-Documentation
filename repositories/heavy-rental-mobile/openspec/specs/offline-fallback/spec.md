# offline-fallback Specification

## Purpose

After a successful login, list and status calls MAY fail. The app SHALL remain usable with seed data and an error banner.

## Requirements

### Requirement: Seed fallback
When list APIs fail, the app SHALL derive deliveries/returns from `MockDataRepository` domain filters.

#### Scenario: Banner
- **GIVEN** `GET /api/deliveries` fails after login
- **WHEN** Deliveries opens
- **THEN** an error banner is shown and seed rows remain visible

### Requirement: Optimistic status
If PATCH fails, the app MAY apply the new status locally without a durable offline queue.

#### Scenario: No Room
- **WHEN** the process is killed
- **THEN** optimistic local status is not required to persist (in-memory v1)
