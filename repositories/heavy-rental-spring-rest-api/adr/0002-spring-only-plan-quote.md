# ADR 0002: Rental-plan quote is Spring arithmetic

- Status: accepted
- Date: 2026-08-21

## Decision
`DefaultPricingClient` uses inclusive day count locally. Haystack is not on the quote path. A Haystack-backed client remains design-only.

## Consequences
Portal quote works when Haystack is down. Pricing ML is not applied to `/quote`.
