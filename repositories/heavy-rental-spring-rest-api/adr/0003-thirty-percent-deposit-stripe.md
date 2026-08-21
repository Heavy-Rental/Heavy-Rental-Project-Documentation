# ADR 0003: 30% Stripe deposit + webhook

- Status: accepted
- Date: 2026-08-21

## Decision
`DEPOSIT_RATE = 0.30`. Create PaymentIntent with off-session setup. Advance booking only after verified webhook. Balance job at 02:00 SGT.

## Consequences
Local checkout needs `stripe listen`. Status will stick at PENDING_DEPOSIT without webhooks.
