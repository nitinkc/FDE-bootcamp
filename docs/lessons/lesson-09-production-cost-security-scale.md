# Lesson 09 — Production AI: Cost, Security & Scale

*Phase 4 · Cost/Security/Scale questions + 6.1, 4.1.*

## Cut LLM App Cost 50% Without Hurting Quality

1. **Measure the breakdown first** — where does spend actually go?
2. **Model routing** — easy queries to cheaper tiers.
3. **Response caching** — identical/similar queries don't re-call the model.
4. **Prompt compaction** — trim boilerplate, summaries instead of raw history.
5. **Batching** where latency allows.
- **Verify with evals** — cost cuts that regress quality don't count.

## Access Control & Data Leakage (6.1)

- **RBAC/ABAC enforced at data + API layers** — never only in the UI; direct
  API calls must hit the same checks.
- **Masking/tokenization/row-level security** for sensitive fields.
- **Least-privilege service accounts**, automated secret rotation.
- **Immutable audit logs** of reads/exports.
- **Red flag:** filtering sensitive records on the frontend.

## Writeback Integrity (4.1)

Console where supervisors click Approve/Reject/Reassign:

- **Optimistic locking** — version stamps/ETags; second approver gets a
  conflict, not silent overwrite. (Or row-level reservation leases.)
- **Idempotent write APIs** — safe to retry.
- **Fast transactional store** for operational state — *separate* from the
  analytical pipeline; don't write clicks to the warehouse.
- **Optimistic UI update** + compensating rollback on failure.
- **Immutable audit log** of every action.
- **Red flag:** writing directly to a data lake on button clicks; no race
  awareness.

## Scaling RAG: 10 → 10,000 Users

What breaks first, in rough order:

- **Model QPS/quota ceilings** — rate limits, provisioned throughput.
- **Index latency under load** — vector store QPS, filtering cost.
- **Cache layers** — embeddings cache, response cache.
- **Autoscaling** stateless serving (Cloud Run), async/non-blocking eval.
- Name specific GCP services when you answer.
