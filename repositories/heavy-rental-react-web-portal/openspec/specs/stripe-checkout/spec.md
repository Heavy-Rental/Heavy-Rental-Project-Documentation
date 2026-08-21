# stripe-checkout Specification

## Purpose

The portal SHALL confirm deposits using Stripe.js/`clientSecret` from Spring. It SHALL NOT hold the Stripe secret key.

## Requirements

### Requirement: Deposit via PaymentIntent
After booking create, the portal SHALL call `POST /api/payments/deposit-intent` and confirm the PaymentIntent client-side.

#### Scenario: Webhook completes status
- **WHEN** Stripe confirms
- **THEN** booking status advances only after Spring processes the webhook (not from client guesswork)
