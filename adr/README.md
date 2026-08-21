# Architecture Decision Records (platform)

Format: [MADR](https://adr.github.io/madr/)-short. Accepted ADRs are immutable. Numbering is monotonic (`NNNN-kebab-title.md`).

## Index

| ID | Title | Status |
|----|-------|--------|
| [0001](./0001-documentation-pack-submission-sot.md) | This pack is the submission documentation SoT | accepted |
| [0002](./0002-dual-mermaid-and-plantuml.md) | UML is published in Mermaid and PlantUML | accepted |
| [0003](./0003-portal-and-mobile-call-spring-only.md) | Portal and mobile call Spring REST only | accepted |
| [0004](./0004-spring-postgres-oltp-source-of-truth.md) | Spring PostgreSQL primary is the OLTP SoT | accepted |
| [0005](./0005-haystack-pull-merge-not-cdc.md) | Haystack fleet mirror is pull-merge, not CDC | accepted |
| [0006](./0006-terraform-creates-ansible-configures.md) | Terraform creates the estate; Ansible only configures guests | accepted |
| [0007](./0007-as-built-specs-label-design-only.md) | Specs are as-built; design-only is labeled | accepted |

Per-repository ADRs: [`../repositories/*/adr/`](../repositories/). Process: [`../docs/spec-governance.md`](../docs/spec-governance.md).
