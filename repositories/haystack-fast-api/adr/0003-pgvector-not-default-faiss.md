# ADR 0003: pgvector, not FAISS

- Status: accepted
- Date: 2026-08-21

## Decision
Durable vectors use pgvector on Haystack Postgres. FAISS is historical.

## Consequences
Primary OLTP stays without the vector extension.
