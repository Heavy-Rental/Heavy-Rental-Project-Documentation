# admin-utilization Specification

## Purpose

`ROLE_ADMIN` SHALL manage users and read trailing six-month fleet utilisation.

## Requirements

### Requirement: Users CRUD
`/api/users` SHALL be ADMIN-only. Create SHALL return a temporary password.

#### Scenario: Non-admin
- **WHEN** a USER calls `GET /api/users`
- **THEN** HTTP 403

### Requirement: Monthly utilisation
`GET /api/monthly-utilization` SHALL return six months of utilisation % and revenue using `UTILIZATION_STATUSES` and inclusive overlap days.

#### Scenario: Consistency
- **THEN** fleet-wide and per-asset views use the same status set
