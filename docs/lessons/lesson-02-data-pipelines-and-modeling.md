# Lesson 02 — Data Pipelines & Entity Modeling

*Phase 1 deep dives 1.2 & 2.1 · Also feeds Phase 4's 2.2 (slow-job debugging).*

## Resilient Ingestion Pipelines

Enterprise data is messy: schemas drift, values go missing, sources rate-limit
and drop. Design for failure:

- **Validate at the boundary** — schema/type checks (e.g., Pydantic) on ingest;
  reject or quarantine bad records early.
- **Decouple** — queues / event-driven patterns absorb bursts and isolate slow
  consumers.
- **Retries with backoff** + **dead-letter queues (DLQs)** — failed records go
  somewhere inspectable, not lost and not blocking the batch.
- **Alerting** — structured alerts on failure rates, lag, DLQ depth.
- **Never assume upstream is clean or documented.**

## Idempotency

The signature follow-up: *"A job crashes mid-way through a 10M-row batch —
re-running must not duplicate records."*

- Give every record a stable natural/dedup key; writes are **upserts**, not
  blind inserts.
- Checkpoint progress (watermarks, processed-batch markers) so re-runs resume,
  not restart.
- Make processing side-effect-free: same input → same result, any number of
  times.

## Operational Entity Modeling

For systems like "Organizations / Facilities / Operators / Equipment / Tasks":

- **Separate mutable state from immutable history** — a current-state view plus
  an append-only event/audit log ("who did what, when").
- **Cardinality** — model the real many-to-many (staff ↔ facilities), don't
  flatten it away.
- **State machines** — tasks have explicit transitions:
  `Pending → In-Progress → Completed / Exception`.
- **Design for query patterns** — shape keys/indexes around the high-frequency
  screens; avoid expensive multi-table joins on hot paths.
- **Extremes to avoid:** one giant denormalized table, or academic
  5th-normal-form nobody can query.
- **Change without rewrites:** e.g., equipment shared across facilities —
  relationship table with validity windows, not schema surgery.

## Diagnostic Debugging (2.2 preview)

Slow job? Inspect first, scale later: execution plans/DAGs → stage timings →
data skew (null keys, hot partitions) → partition pruning → incremental
watermarks. **"Add more nodes" is a red-flag answer.**
