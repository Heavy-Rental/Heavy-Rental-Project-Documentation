# documentation-governance Specification

## Purpose

This pack SHALL document as-built behavior using OpenSpec, OpenSPDD, and ADR, without silently mixing design-only work into the as-built narrative.

## Requirements

### Requirement: Three-layer spec model
Behavior-changing documentation SHALL use OpenSpec (what), OpenSPDD REASONS Canvas (how / not-how), and ADR (why).

#### Scenario: Layer locations
- **WHEN** a contributor adds a platform decision
- **THEN** they add or update `openspec/specs/`, `spdd/prompt/`, and `adr/` according to [`docs/spec-governance.md`](../../../docs/spec-governance.md)

### Requirement: As-built vs design-only
Specs SHALL describe implemented behavior. Unbuilt items SHALL be listed as design-only.

#### Scenario: Depots stub
- **GIVEN** `GET /api/depots`
- **WHEN** documenting the equipment page
- **THEN** the spec states the route returns an empty array and that no Depot entity exists

### Requirement: Immutable ADRs
Accepted ADRs SHALL NOT be edited in place. A new ADR SHALL supersede the old file.

#### Scenario: Changing a decision
- **WHEN** the team reverses a durable choice
- **THEN** a new `NNNN-kebab-title.md` is added with `Supersedes:` pointing at the previous ADR
