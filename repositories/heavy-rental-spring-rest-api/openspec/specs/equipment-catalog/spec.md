# equipment-catalog Specification

## Purpose

Authenticated users SHALL list, filter, and (where allowed) mutate fleet assets.

## Requirements

### Requirement: List with optional availability window
`GET /api/equipment` SHALL support `category`, `search`, `condition`, and optional `startDate`/`endDate`. When dates are supplied, `available` SHALL reflect overlap with **ACTIVE_STATUSES**.

#### Scenario: Images
- **THEN** `img` is a JPEG data URI `data:image/jpeg;base64,...` when an image exists

### Requirement: Depots stub
`GET /api/depots` SHALL return `[]`. There is no Depot entity.

#### Scenario: Frontend does not 500
- **WHEN** the equipment page also requests depots
- **THEN** the response is an empty JSON array
