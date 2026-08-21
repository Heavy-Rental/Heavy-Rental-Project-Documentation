# Specifications — heavy-rental-spring-rest-api

Upstream: [Heavy-Rental/heavy-rental-spring-rest-api](https://github.com/Heavy-Rental/heavy-rental-spring-rest-api) (`develop`).  
Authenticated OLTP API. As-built HTTP: upstream `DOCUMENTATION.md` and `openspec/specs/`.

| Layer | Path |
|-------|------|
| OpenSpec | [`openspec/`](openspec/) |
| OpenSPDD | [`spdd/`](spdd/) |
| ADR | [`adr/`](adr/) |

## Capabilities

| Spec | Summary |
|------|---------|
| [auth-jwt](openspec/specs/auth-jwt/spec.md) | Interim mint, login, logout, denylist |
| [equipment-catalog](openspec/specs/equipment-catalog/spec.md) | Fleet list/filter/CRUD |
| [rental-plan-quote](openspec/specs/rental-plan-quote/spec.md) | Spring-only plan quote |
| [booking-payments](openspec/specs/booking-payments/spec.md) | Bookings, 30% deposit, Stripe |
| [delivery-return](openspec/specs/delivery-return/spec.md) | Ops status machine |
| [haystack-recommender](openspec/specs/haystack-recommender/spec.md) | Dual-hop saga |
| [admin-utilization](openspec/specs/admin-utilization/spec.md) | Users and utilisation |
