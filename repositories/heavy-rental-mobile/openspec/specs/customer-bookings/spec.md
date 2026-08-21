# customer-bookings Specification

## Purpose

`ROLE_USER` sessions SHALL view their bookings and MUST NOT update delivery/return status in the app.

## Requirements

### Requirement: Read-only list
The Customer Bookings screen SHALL load `GET /api/bookings` and allow status filters without edit affordances.

#### Scenario: No mobilise button
- **GIVEN** a customer session
- **WHEN** a booking is `CONFIRMED`
- **THEN** the UI does not expose PATCH delivery/return
