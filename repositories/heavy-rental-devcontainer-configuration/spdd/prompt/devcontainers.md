# REASONS Canvas — DevContainers

## R — Requirements
Reproducible local stacks for REST, Haystack, Portal.

## E — Entities
Compose services listed in ARCHITECTURE.md (app, postgres-primary, replica, postgres-haystack, sync, neo4j, populate).

## A — Approach
External network; promote REST `.devcontainer`; pull-merge not CDC.

## S — Structure
Three folders under the configuration repo.

## O — Operations
See [`QUICKSTART.md`](../../../QUICKSTART.md) bring-up order.

## N — Norms
Dev credentials only (`postgres`/`postgres`, Neo4j `neo4j`/`heavyrental`).

## S — Safeguards
- MUST NOT put pgvector on primary.
- MUST NOT let Haystack write primary.
- MUST NOT require a single compose file for all three packs.
