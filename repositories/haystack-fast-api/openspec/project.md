# OpenSpec — haystack-fast-api

Python 3.12, uv, FastAPI port 8000. No public auth (Spring is the façade). Sessions are process-local: Call 2 needs Call 1 `ingest_id` on the same process.
