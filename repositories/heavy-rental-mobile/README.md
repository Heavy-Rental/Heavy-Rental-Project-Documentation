# Specifications — heavy-rental-mobile

Upstream: [Heavy-Rental/heavy-rental-mobile](https://github.com/Heavy-Rental/heavy-rental-mobile) (`develop`).  
Android operations app: today’s deliveries and returns, plus read-only customer bookings.

| Layer | Path |
|-------|------|
| OpenSpec | [`openspec/`](openspec/) |
| OpenSPDD | [`spdd/`](spdd/) |
| ADR | [`adr/`](adr/) |
| Upstream SDD | `specification/` in the product repo |

## Capabilities

| Spec | Summary |
|------|---------|
| [auth-login](openspec/specs/auth-login/spec.md) | Interim → access JWT; staff vs customer routing |
| [home-dashboard](openspec/specs/home-dashboard/spec.md) | Today’s delivery/return counts |
| [deliveries-returns](openspec/specs/deliveries-returns/spec.md) | Lists, maps, mobilise/complete |
| [customer-bookings](openspec/specs/customer-bookings/spec.md) | `ROLE_USER` read-only bookings |
| [offline-fallback](openspec/specs/offline-fallback/spec.md) | Seed data and optimistic PATCH |
