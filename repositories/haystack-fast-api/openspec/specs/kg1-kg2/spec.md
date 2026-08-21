# kg1-kg2 Specification

## Purpose

One Neo4j instance SHALL host KG-1 DocumentStore (`:Document`) and KG-2 fleet (`:Asset` `:Booking` `:Category`) without populate dropping KG-1.

## Requirements

### Requirement: Populate isolation
`neo4j-populate` SHALL MERGE fleet labels and SHALL NEVER drop `:Document` nodes.

#### Scenario: Trigger failure
- **WHEN** populate HTTP fails
- **THEN** SQL merge still succeeds
