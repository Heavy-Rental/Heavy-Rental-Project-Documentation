# REASONS Canvas — pipeline

## R — Requirements
Build, test, publish, and redeploy each app.

## E — Entities
GitHub Actions workflows, GHCR/ECR tags, Ansible limits.

## A — Approach
Fast-feedback + full CI + release. Infra repo owns first `deploy-projects`.

## S — Structure
`.github/workflows/` plus per-app pipeline folders.

## O — Operations
PR → CI; tag → release image; CD caller → Ansible `--limit`.

## N — Norms
New tags per redeploy.

## S — Safeguards
- MUST NOT create IAM or VPC from app CD.
- MUST NOT treat this repo as product OpenSpec for bookings/recommend.
