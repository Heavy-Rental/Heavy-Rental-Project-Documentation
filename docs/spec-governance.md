# Spec governance: OpenSpec, OpenSPDD, and ADR

This documentation repository is the **submission SoT** for Heavy Rental system design. Product HTTP contracts still live in each application repo; this pack synthesizes as-built behavior and must stay consistent with `develop` on those remotes.

## The three layers

| Layer | Tool | Answers | Lives in |
|-------|------|---------|----------|
| **What** | [OpenSpec](https://github.com/Fission-AI/OpenSpec) | Current agreed **behavior** | `openspec/specs/` and `repositories/<repo>/openspec/specs/` |
| **How / not-how** | [OpenSPDD](https://github.com/gszhangwei/open-spdd) REASONS Canvas | Implementation contract and safeguards | `spdd/` and `repositories/<repo>/spdd/` |
| **Why** | [ADR](https://adr.github.io/) (MADR-short) | Durable architectural choice | `adr/` and `repositories/<repo>/adr/` |

```text
                    ┌─────────────────────────────────────────┐
                    │  adr/     WHY (architecture memory)      │
                    │  OpenSpec WHAT (behavior SoT)            │
                    │  OpenSPDD HOW (REASONS Canvas contract)  │
                    └─────────────────────────────────────────┘
                                      ▲
                     OpenSpec change: proposal → specs → design → adr → tasks
```

Schema: **`spec-driven-with-adr`**. Artifact order: proposal → specs → design → adr → tasks.

## Rules

1. Requirements use `### Requirement:` plus at least one `#### Scenario:` with GIVEN / WHEN / THEN.
2. Specs describe **as-built** observable behavior. Label design-only items explicitly.
3. Accepted ADRs are **immutable**. Supersede with a new file; never edit Status or body of an accepted ADR.
4. OpenSPDD Safeguards are the negative space (what MUST NOT be done).
5. UML in specs uses Mermaid and/or PlantUML. Platform diagrams also live in `docs/diagrams/`.
6. Skip a full change folder only for typo/docs-only edits.

## Reading order

1. [`DOCUMENTATION.md`](../DOCUMENTATION.md)
2. [`QUICKSTART.md`](../QUICKSTART.md)
3. [`adr/README.md`](../adr/README.md)
4. OpenSpec for the repository you are changing
5. Matching OpenSPDD canvas

## Optional CLI

Installing `openspec` or `openspdd` is optional. Markdown in this repository is the contract.
