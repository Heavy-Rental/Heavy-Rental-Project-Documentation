# app-cd Specification

## Purpose

Day-two image rolls SHALL use Ansible on existing guests, not Terraform apply.

## Requirements

### Requirement: Academy callers
Workflows such as `portal-cd-academy-caller` and `web-portal-cd-academy` SHALL deploy a single app image to the estate.

#### Scenario: No VPC create
- **THEN** CD does not create ASGs or RDS
