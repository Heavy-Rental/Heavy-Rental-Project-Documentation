# delivery-return Specification

## Purpose

Ops APIs SHALL advance `CONFIRMED → MOBILISED` and `MOBILISED → COMPLETED` only.

## Requirements

### Requirement: Today deliveries
`GET /api/deliveries` SHALL return bookings with `startDate == today` and status CONFIRMED or MOBILISED.

#### Scenario: Mobilise
- **WHEN** `PATCH /api/deliveries/{id}/status` body is `{ "bookingStatus": "MOBILISED" }` and current status is CONFIRMED
- **THEN** status becomes MOBILISED; other transitions return 400

### Requirement: Today returns
`GET /api/returns` SHALL return today’s due returns. Complete SHALL require MOBILISED → COMPLETED.

#### Scenario: Optional notes
- **THEN** `returnNotes` MAY be stored on complete
