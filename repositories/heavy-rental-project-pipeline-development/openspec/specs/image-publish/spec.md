# image-publish Specification

## Purpose

Release workflows SHALL publish container (or mobile) artifacts with **new tags** for deploy.

## Requirements

### Requirement: Release workflows
`mobile-release`, `rest-api-release`, and `web-portal-release` SHALL exist for tagged/release events.

#### Scenario: No silent latest-only
- **THEN** operators prefer a new tag so compose does not rely on `--pull always`
