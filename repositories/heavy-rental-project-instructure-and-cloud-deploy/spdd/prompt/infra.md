# REASONS Canvas — Academy infra

## R — Requirements
Lab-safe two-AZ estate for portal, REST, Haystack, Neo4j, two RDS.

## E — Entities
VPC, NAT GW, ASG, ALB, NLB, RDS Multi-AZ, Secrets Manager shells.

## A — Approach
Terraform create; Ansible configure; pipeline CD for images.

## S — Structure
`terraform/academy/`, `ansible/`, `docs/`.

## O — Operations
bootstrap → plan → apply → deploy-projects → later app CD. stop pauses ASG/RDS. destroy tears down.

## N — Norms
Image refs from GitHub Environment `PORTAL_IMAGE` / `REST_IMAGE` / `HAYSTACK_IMAGE`.

## S — Safeguards
- MUST NOT create IAM on Academy.
- MUST NOT use Ansible to create VPC/ASG/RDS.
- MUST NOT assume Neo4j is a causal cluster.
- MUST NOT expect `stop` to pause NAT Gateway billing.
