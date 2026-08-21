# ADR 0002: Dual Mermaid and PlantUML

- Status: accepted
- Date: 2026-08-21

## Context

GitHub renders Mermaid in markdown. Academic/tooling reviewers often expect PlantUML for UML.

## Decision

Publish each major diagram in **both** Mermaid (inline in `DOCUMENTATION.md`) and PlantUML (fences + `docs/diagrams/*.puml`). Do not pre-render PNG as a requirement.

## Consequences

- Two sources to keep in sync.
- GitHub preview works without extra plugins; PlantUML needs a previewer.
