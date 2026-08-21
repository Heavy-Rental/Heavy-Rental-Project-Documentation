# web-portal-pack Specification

## Purpose

The portal pack SHALL be a Node/Vite workspace with no local database.

## Requirements

### Requirement: Peer API
Product HTTP SHALL be configured toward Spring (`heavy-rental-rest-api:8080` or localhost:8080). The pack MAY start without Spring.

#### Scenario: No Haystack credentials
- **THEN** Compose does not inject Haystack secrets into the portal
