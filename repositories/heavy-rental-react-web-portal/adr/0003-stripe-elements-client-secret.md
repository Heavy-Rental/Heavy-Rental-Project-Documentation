# ADR 0003: Stripe via clientSecret

- Status: accepted
- Date: 2026-08-21

## Decision
Portal confirms PaymentIntents with the publishable key and server-issued `clientSecret`.

## Consequences
Webhook remains mandatory for booking status.
