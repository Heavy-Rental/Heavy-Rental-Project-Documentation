# ADR 0007: Specs are as-built; design-only is labeled

- Status: accepted
- Date: 2026-08-21

## Context

OpenSpec changes such as `pricing-estimate` exist but are not implemented. Mixing them into route tables would fail examiners and integrators.

## Decision

Submission specs and `DOCUMENTATION.md` describe implemented behavior. Unbuilt items go in an explicit design-only section.

## Consequences

- Readers can trust endpoint tables.
- Design work remains visible without being mistaken for production.
