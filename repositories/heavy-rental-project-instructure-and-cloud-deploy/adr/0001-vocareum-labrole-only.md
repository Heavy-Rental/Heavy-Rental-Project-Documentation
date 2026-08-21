# ADR 0001: Vocareum LabRole only

- Status: accepted
- Date: 2026-08-21

## Decision
Every Academy EC2 uses `LabInstanceProfile` → `LabRole`. Terraform does not create IAM.

## Consequences
Fits Academy rules; paid AWS_ACTUAL path may create instance profiles later.
