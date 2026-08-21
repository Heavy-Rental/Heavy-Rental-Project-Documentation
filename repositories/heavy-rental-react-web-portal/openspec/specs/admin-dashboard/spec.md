# admin-dashboard Specification

## Purpose

Admin sessions SHALL manage fleet, bookings, and view utilisation charts from Spring admin APIs.

## Requirements

### Requirement: Role-gated dashboard
`ROLE_ADMIN` SHALL reach admin routes. User APIs and monthly utilisation SHALL be requested with the access JWT.

#### Scenario: Employee overview
- **THEN** an employee dashboard MAY show operational overview without user CRUD
