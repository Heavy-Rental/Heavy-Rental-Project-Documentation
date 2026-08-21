# ADR 0002: Terraform creates; Ansible configures

- Status: accepted
- Date: 2026-08-21

## Decision
Split create vs configure. Ansible never owns VPC/ASG/RDS lifecycle.

## Consequences
Clear `destroy` path; configure-only is safe after apply.
