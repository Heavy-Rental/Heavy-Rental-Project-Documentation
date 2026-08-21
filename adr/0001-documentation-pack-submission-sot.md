# ADR 0001: Documentation pack is the submission source of truth

- Status: accepted
- Date: 2026-08-21
- Deciders: Heavy Rental documentation team

## Context

Product behavior is specified inside each Git repository. Examiners need one pack that maps all repos, features, and UML without cloning seven codebases.

## Decision

Keep a dedicated `Heavy-Rental-Project-Documentation` repository as the **submission SoT**. Synthesize as-built OpenSpec / OpenSPDD / ADR here. Link, do not replace, product-repo contracts on `develop`.

## Consequences

- Duplication risk: this pack can drift from product repos.
- Benefit: one reading path for submission (`DOCUMENTATION.md` + `repositories/`).
- Update this pack when product OpenSpec is archived.
