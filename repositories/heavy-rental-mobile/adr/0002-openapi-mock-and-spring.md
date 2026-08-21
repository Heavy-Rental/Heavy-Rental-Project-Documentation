# ADR 0002: OpenAPI mocks plus real Spring

- Status: accepted
- Date: 2026-08-21

## Context
Demos must run without a backend; production-like demos need Spring.

## Decision
Keep OpenAPI-driven Mockoon/Prism on `:8081` and default `USE_MOCK_SERVER=false` (Spring `:8080`).

## Consequences
Two base URLs; Mockoon does not validate credentials the way Spring does.
