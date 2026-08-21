# terraform-academy Specification

## Purpose

Terraform SHALL create VPC, two NAT Gateways, four ASG roles (portal, rest, haystack, neo4j), ALBs, two Multi-AZ RDS, Bolt NLB, and secret shells.

## Requirements

### Requirement: Apply does not pull app images
`action=apply` SHALL run Terraform then `configure.yml` (Docker + Neo4j compose). Portal/REST/Haystack first compose SHALL wait for `action=deploy-projects`.

#### Scenario: LabRole
- **THEN** guests use LabInstanceProfile; Terraform does not create IAM on Academy
