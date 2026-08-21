# ADR 0006: Terraform creates the estate; Ansible only configures guests

- Status: accepted
- Date: 2026-08-21

## Context

Academy labs forbid creating IAM. Mixing resource create into Ansible makes destroy/plan harder.

## Decision

Terraform owns VPC, NAT Gateways, ASGs, ALBs, RDS, NLB, and secret shells. Ansible installs Docker, writes `.env` from Secrets Manager, and runs compose on **existing** guests. `deploy-projects` is a later Action after `apply`.

## Consequences

- Clear operate path (`OPERATOR-GUIDE.md` actions).
- App CD can redeploy images without Terraform.
