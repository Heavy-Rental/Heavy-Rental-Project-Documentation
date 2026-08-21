# call3-knowledge Specification

## Purpose

Call 3 SHALL answer questions against the same ingest session without re-running Call 1 or Call 2.

## Requirements

### Requirement: Query
`POST /internal/v1/recommendations/project-knowledge/query` SHALL return `answer` and `sourcesUsed`.

#### Scenario: No quote mutation
- **THEN** the response does not replace the stored quote `items[]`
