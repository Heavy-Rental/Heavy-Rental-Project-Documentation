# ADR 0004: deploy-projects after apply

- Status: accepted
- Date: 2026-08-21

## Decision
First portal/REST/Haystack compose is a later `action=deploy-projects` (`site.yml`), not the end of apply.

## Consequences
Apply can finish with Neo4j-only compose; images must exist in GHCR/ECR before deploy-projects.
