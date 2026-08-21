# rental-plan-quote Specification

## Purpose

A customer SHALL have at most one active (DRAFT/SAVED/QUOTED) plan. Quote math SHALL be Spring-only.

## Requirements

### Requirement: Inclusive day quote
`POST /api/rentalPlans/{id}/quote` SHALL compute `days = ChronoUnit.DAYS.between(start, end) + 1` and `subtotal = baseDailyRate × days`. It SHALL NOT call Haystack.

#### Scenario: Second active plan
- **WHEN** a customer already has DRAFT/SAVED/QUOTED
- **THEN** another create returns `409 conflict`

### Requirement: Postal site address
Create SHALL require `siteAddress` ending in a 6-digit postal code.

#### Scenario: Invalid postal
- **THEN** HTTP 400 `validation_failed`
