# platform-overview Specification

## Purpose

The Heavy Rental platform SHALL present a single rental product across web, mobile, REST, and an internal recommender, with supporting DevContainer, CI/CD, and AWS Academy infrastructure.

## Requirements

### Requirement: Multi-repository product surface
The platform SHALL consist of the Android app, React web portal, Spring REST API, and Haystack FastAPI as product repositories, plus DevContainer, pipeline, and infra supporting repositories.

#### Scenario: Repository map present
- **GIVEN** the documentation pack
- **WHEN** a reader opens `DOCUMENTATION.md`
- **THEN** all seven GitHub repositories are listed with role and stack

### Requirement: Spring is the only public HTTP backend
The browser and the Android app SHALL call Spring REST for product flows. They SHALL NOT call Haystack, Postgres, or Neo4j directly.

#### Scenario: Recommend via dual-hop
- **GIVEN** a signed-in portal user
- **WHEN** they submit a project specification
- **THEN** the portal sends JWT HTTP to Spring, and Spring calls Haystack Call 1 then Call 2

### Requirement: OLTP write ownership
PostgreSQL primary used by Spring SHALL be the only writer of product fleet and booking rows. Haystack SHALL pull a mirror and SHALL NOT write the primary.

#### Scenario: Primary down during sync
- **GIVEN** Haystack merge-sync is running
- **WHEN** `postgres-primary` is unreachable
- **THEN** the sync job skips the cycle and retains local Haystack rows (default)

### Requirement: Submission UML
The documentation pack SHALL include use case, sequence, and entity-relationship diagrams in both Mermaid and PlantUML.

#### Scenario: Dual diagram languages
- **GIVEN** `DOCUMENTATION.md` and `docs/diagrams/`
- **WHEN** a reviewer inspects architecture sections
- **THEN** Mermaid blocks and matching `.puml` files exist for context, use cases, auth/booking/recommender sequences, ERD, and Academy deployment
