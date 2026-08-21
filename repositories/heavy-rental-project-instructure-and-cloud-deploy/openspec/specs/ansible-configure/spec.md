# ansible-configure Specification

## Purpose

Ansible SHALL configure existing guests only: Docker, Secrets Manager → `.env`, compose.

## Requirements

### Requirement: No resource create
Playbooks SHALL NOT create VPC, ASG, or RDS.

#### Scenario: configure-only
- **WHEN** `action=configure-only`
- **THEN** Terraform apply is skipped and the same configure playbook runs
