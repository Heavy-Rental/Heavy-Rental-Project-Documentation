# OpenSpec — Heavy Rental documentation pack

| Field | Value |
|-------|--------|
| **Module** | `Heavy-Rental-Project-Documentation` |
| **Schema** | `spec-driven-with-adr` |
| **Purpose** | Submission SoT for all product and supporting Git repositories |

## Constitution

| Topic | Rule |
|-------|------|
| Clients | Portal and Android call **Spring REST only** |
| OLTP | `postgres-primary` is the only product writer |
| Haystack | Internal dual-hop from Spring; never invent catalog on failure |
| Diagrams | Mermaid + PlantUML for submission UML |
| Specs | As-built; design-only labeled |

## Living capabilities

| Capability | Path |
|------------|------|
| Platform overview | [`specs/platform-overview/spec.md`](specs/platform-overview/spec.md) |
| Documentation governance | [`specs/documentation-governance/spec.md`](specs/documentation-governance/spec.md) |

Per-repository specs: [`../repositories/`](../repositories/).
