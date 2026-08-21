# ci-build-test Specification

## Purpose

Each product app SHALL have a fast-feedback workflow and a full CI workflow on pull requests.

## Requirements

### Requirement: Per-app CI
The pipeline repo SHALL provide `mobile-fast-feedback` / `mobile-ci`, `rest-api-fast-feedback` / `rest-api-ci`, and `web-portal-fast-feedback` / `web-portal-ci`.

#### Scenario: PR
- **WHEN** a PR targets the relevant app
- **THEN** fast-feedback runs a shorter check and full CI runs the complete suite
