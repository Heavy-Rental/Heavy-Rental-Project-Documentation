# OpenSpec — heavy-rental-spring-rest-api

| Field | Value |
|-------|--------|
| Package | `com.heavy_rental.rest_api` |
| Stack | Java 21, Spring Boot 4.1, PostgreSQL, JWT HS256, Stripe, Resilience4j |
| Port | 8080 |

## Constitution

- PostgreSQL only (no H2 default). Thin controllers. Shared `{error, message}` JSON.
- Prod: Flyway + `ddl-auto=validate`. Dev: Hibernate update + `data.sql`.
- Never invent equipment on Haystack failure.
