# Phase 4 — Production-Grade AI Platforms

**Goal:** Operate AI systems in production environments.

## Master
- [ ] Monitoring
- [ ] Observability
- [ ] Evaluation Pipelines
- [ ] Tracing
- [ ] Cost Optimization
- [ ] Reliability
- [ ] Security
- [ ] Scalability

## Self-Interview Check

Ask each question **cold and out loud** (~2–3 min each). Score honestly:
**1** = couldn't answer · **3** = partial / hand-wavy · **5** = crisp with production depth.
Questions marked §x.x are expanded in the [Interview Deep Dive](#interview-deep-dive) below.

### Reliability & Debugging

1. **"An ingestion job that used to take 25 minutes now takes 4 hours. Walk me through your diagnostic workflow."** *(§2.2)*
   - Strong answer: execution plans/DAGs, stage timings, data skew, partition pruning, incremental watermarks — never "add more nodes" first.
2. **"Your LLM endpoint's p95 latency tripled overnight. How do you triage?"**
   - Strong answer: splits model vs. retrieval vs. orchestration time via traces, checks token counts, cold starts, upstream changes.
3. **"An automated pipeline produces anomalous output at 2 a.m. How does the frontline workflow keep running?"** *(§6.2)*
   - Strong answer: circuit breakers, last-known-good/cached fallback, rule-based degrade path, human escalation queue, on-call alert.

### Observability & Evaluation Pipelines

1. **"What do you monitor for an AI service that you wouldn't monitor for a normal API?"**
   - Strong answer: quality/eval metrics, drift, hallucination or override rates, per-request cost, token usage, tool-call success rates — plus the usual golden signals.
2. **"Design an evaluation pipeline that gates every prompt, model, or retrieval change before it ships."**
   - Strong answer: versioned eval sets, automated scoring in CI, thresholds, human spot-checks, rollback path.
3. **"How do you trace a multi-step agent or RAG request end-to-end in production?"**
   - Strong answer: OpenTelemetry spans per LLM/tool/retrieval call, trace IDs tied to user feedback, per-span cost and latency.

### Cost, Security & Scale

1. **"Leadership asks you to cut this LLM app's cost by 50% without hurting quality. How?"**
   - Strong answer: measure cost breakdown first, then model routing to cheaper tiers, response caching, prompt compaction, batching — verified by evals.
2. **"How do you enforce least-privilege access and prevent sensitive data leaking across user tiers — end to end?"** *(§6.1)*
   - Strong answer: RBAC/ABAC enforced at data and API layers (not just UI), masking/row-level security, least-privilege service accounts, audit logs.
3. **"Field supervisors click Approve/Reject on flagged records. Architect the writeback: consistency, race conditions, immediate UI freshness."** *(§4.1)*
   - Strong answer: optimistic locking (versions/ETags), idempotent write APIs, immutable audit log, transactional store separate from analytical pipeline.
4. **"Your RAG app grows from 10 to 10,000 users. What breaks first, and how do you scale it?"**
    - Strong answer: model QPS/quota ceilings, index latency under load, cache layers, autoscaling, async eval — with specific GCP choices.

### Phase Gate

- [ ] Scored **4+ on ≥80%** of the questions above, out loud, without notes.
- [ ] Production hardening pass done on the Healthcare RAG Platform.

## Interview Deep Dive

*Full interviewer context for the §-marked questions above — what's actually being tested.*

### §2.2 — Distributed Computing & Diagnostic Troubleshooting

- **Question:** "Imagine you have an ETL job processing tens of millions of records daily that has steadily slowed down from 25 minutes to over 4 hours. Walk me through your diagnostic workflow to identify the root bottleneck and remediate it."
- **Good signs:** systematically checks query execution plans (DAGs), I/O wait times, memory allocation, and stage breakdowns; understands data skew (null keys, high-cardinality values causing single-worker stragglers); recommends concrete fixes — broadcast joins for small lookup tables, salting skewed keys, partition pruning, or converting full scans into watermark-based incremental pipelines.
- **Red flags:** immediately suggests scaling up cluster hardware ("add more nodes or RAM") without inspecting query plans, partition distributions, or memory leaks.

### §4.1 — Two-Way Data Flow & Writeback Integrity

*In FDE work, data flows bidirectionally — users take actions that write back to transactional engines.*

- **Question:** "You build an operational console where field supervisors review flagged records and click 'Approve', 'Reject', or 'Reassign'. How do you architect the writeback mechanism to ensure consistency, prevent race conditions (two supervisors simultaneously approving the same record), and ensure the UI reflects changes immediately without waiting hours for an analytical pipeline to re-run?"
- **Good signs:** concurrency control via optimistic locking (version stamps, ETags) or row-level reservation leases; decouples real-time operational state (fast transactional store/API) from downstream analytical pipelines; optimistic UI updates backed by compensating rollback transactions; idempotent writeback APIs with immutable audit logs.
- **Red flags:** proposes writing directly to a data lake or analytical warehouse table on button clicks; no awareness of race conditions or data locking.

### §6.1 — Data Security, Access Control & Permission Boundaries

- **Question:** "When building data pipelines and operational tools that handle sensitive customer, employee, or financial data, what architectural steps do you take to enforce strict access control and prevent data leakage across different user tiers?"
- **Good signs:** ABAC or RBAC enforced at the data storage and API gateway layers, not just frontend UI logic; data masking, tokenization, or row-level security for sensitive fields; least-privilege service credentials, automated secret rotation, immutable audit logs of read/export actions.
- **Red flags:** suggests filtering sensitive records solely on the frontend client; no understanding of how data access can be bypassed via direct API calls.

### §6.2 — Designing Fail-Safes and Safe Defaults

- **Question:** "If an automated ingestion pipeline or backend scoring service fails in production or produces anomalous outputs, how do you ensure the frontline business workflow does not grind to a complete halt?"
- **Good signs:** automated fallback paths — graceful degradation to rule-based defaults or last-known-good cached data; circuit breakers that pause automated actions when anomaly rates exceed a threshold; human-in-the-loop escalation queues and instant notification for on-call engineers.
- **Red flags:** believes high availability means "the code never fails"; no contingency plan for partial outages or data anomalies.

## Notes / Evidence
