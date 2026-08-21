# home-dashboard Specification

## Purpose

Staff Home SHALL show today’s delivery and return counts by status.

## Requirements

### Requirement: Today counts
After login, the app SHALL load `GET /api/deliveries` and `GET /api/returns` and display counts for today’s work.

#### Scenario: Empty today
- **GIVEN** both endpoints return empty arrays
- **WHEN** Home renders
- **THEN** counts are zero and the UI remains usable
