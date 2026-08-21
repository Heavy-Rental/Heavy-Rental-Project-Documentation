# project-spec-assistant Specification

## Purpose

The equipment assistant SHALL submit project text/file to Spring `POST /api/recommendations/project-spec` and display the quote. It SHALL NOT call Haystack.

## Requirements

### Requirement: Quote then optional Q&A
Submit SHALL return quote `items[]`. Follow-up questions SHALL use `POST /api/recommendations/{id}/knowledge-query`.

#### Scenario: Haystack down
- **THEN** the UI shows Spring `recommender_*` errors and does not invent equipment cards
