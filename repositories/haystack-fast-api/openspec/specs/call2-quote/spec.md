# call2-quote Specification

## Purpose

Call 2 SHALL return an equipment **quote** (`items[]`), not a chatbot answer.

## Requirements

### Requirement: Session quote
`POST /internal/v1/recommendations/project-knowledge/getassetrecommendations` SHALL require a prior Call 1 `ingest_id` on the same process.

#### Scenario: Missing session
- **THEN** HTTP 404

### Requirement: Live identity
When `FLEET_BACKEND=sql`, `equipment.id` SHALL be `assets.id` (string). Missing assets SHALL be omitted. The live path SHALL NOT fall back to seed `AST-*` ids.

#### Scenario: Fake backend
- **WHEN** `FLEET_BACKEND=fake`
- **THEN** seed catalog ids may look like `AST-*`
