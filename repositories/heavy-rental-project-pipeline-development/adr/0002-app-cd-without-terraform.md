# ADR 0002: App CD without Terraform

- Status: accepted
- Date: 2026-08-21

## Decision
Image redeploys use Ansible on guests created by the infra repo.

## Consequences
Faster rolls; first estate still needs infra `apply` + `deploy-projects`.
