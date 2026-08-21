# public-catalog Specification

## Purpose

Anonymous and signed-in users SHALL browse equipment with search and filters.

## Requirements

### Requirement: Catalog UI
The public portal SHALL show catalog, search/filter, hero, stats, and testimonials.

#### Scenario: API mode
- **WHEN** `npm run dev:api` is used
- **THEN** list data comes from Spring `GET /api/equipment`
