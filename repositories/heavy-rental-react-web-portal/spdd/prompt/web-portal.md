# REASONS Canvas — React web portal

## R — Requirements
Public catalog, customer checkout, admin dashboards, Stripe deposit UI, project-spec assistant.

## E — Entities
`App`, `CustomerOnboarding`, `AdminDashboard`, `AuthContext`, `ApiClient`.

## A — Approach
Vite proxy. JWT stored for API calls. Stripe publishable key only.

## S — Structure
`src/app/*` screens; `src/styles/theme.css` tokens.

## O — Operations
1. Login (interim + access). 2. Browse. 3. Plan/cart. 4. Booking + PaymentIntent. 5. Optional project-spec.

## N — Norms
TypeScript. `dev:mock` vs `dev:api` env files.

## S — Safeguards
- MUST NOT call Haystack from the browser.
- MUST NOT embed Stripe secret keys.
- MUST NOT treat mock API as production SoT.
