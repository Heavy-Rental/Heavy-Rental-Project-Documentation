# REASONS Canvas — haystack-fast-api

## R — Requirements
Call 1 ingest, Call 2 quote, Call 3 Q&A; honest ids and rates.

## E — Entities
Ingest session, DocumentStore, FleetBackend (fake|sql), Neo4j KG-1/KG-2.

## A — Approach
uv + uvicorn. Config via `.env`. Spring dual-hop is the product path.

## S — Structure
`app/main.py` routes → services/pipelines/agents.

## O — Operations
1. Health. 2. Call 1. 3. Call 2 with ingest_id. 4. Optional Call 3.

## N — Norms
Pytest ignores host `.env` fleet settings. Correlation header.

## S — Safeguards
- MUST NOT invent fleet ids, rates, dates, or budgets.
- MUST NOT write postgres-primary.
- MUST NOT drop KG-1 `:Document` during populate.
- MUST NOT expose these routes as the browser API.
