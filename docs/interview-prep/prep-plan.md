# Prep Plan — Question → Concept Map

Reverse-engineered from the phase self-interview banks and their interview deep dives.
Every question is decomposed into the **atomic concepts** a Level-5 answer requires.

## How to use this

1. **Scan each concept line.** Mark it: `✅` solid · `⚠️` fuzzy · `❌` gap.
2. Each concept has a **gap signal** — the litmus test. If you can't pass it
   out loud in ~30 seconds, it's a gap even if the term feels familiar.
3. Collect all `❌`/`⚠️` items → that's your study list. Ask for detail on
   those specific concepts (nothing else).
4. Classify each gap before studying it:

| Gap type | What it means | How to close |
|---|---|---|
| **K** — Knowledge | You've never learned it | Read / ask for an explainer |
| **H** — Hands-on | You know the theory, never built it | Build it in the RAG project or a drill — can't be faked verbally |
| **A** — Articulation | You know it, can't say it crisply | Out-loud reps, write an "Interview-Ready Explanation" in your notes |

5. Priority order follows the interviewer scorecard weights (§9, Phase 6):
   **Production Engineering 25% → Data Modeling & Compute 20% → Stakeholder & Scoping 20% → Accountability & GSD 20% → Applied AI 15%.**
   A gap in a 25% pillar beats two gaps in a 15% pillar.

---

## Section A — Production Engineering (25% weight)

### Q: Notebook → production service *(§1.1, Phase 1)*

- [ ] Modular project layout vs. notebook script — *signal: can you describe src/tests/entrypoint separation in 30s?*
- [ ] API contract design — typed request/response schemas (Pydantic), versioning
- [ ] Test pyramid — what gets unit vs. integration tests vs. none; contract/boundary tests *(Phase 1 SWE Q3)*
- [ ] Containerization — Dockerfile hygiene, image size, non-root, multi-stage builds
- [ ] CI/CD stages — lint → test → build → deploy; what gates what
- [ ] Structured logging & telemetry — log levels, correlation IDs, what you'd instrument
- [ ] Dependency management — pinning, lockfiles, env separation, secrets out of code
- [ ] Handoff readiness *(probe)* — README/runbook, typed interfaces, tests as docs. *Signal: describe a real 24h onboarding cold.*
- [ ] Debugging a prod bug you can't repro *(Phase 1 SWE Q4)* — logs/traces first, bisect deploys/config, staging repro, fix + regression test

### Q: Ingestion pipeline across messy legacy systems *(§1.2, Phase 6 SD drill)*

- [ ] Validation at the boundary — schema contracts, rejecting/quarantining bad records early
- [ ] Idempotency — dedup keys, upserts, why re-runs must not double-write
- [ ] Retry semantics — backoff + jitter, what's retryable vs. poison
- [ ] Dead-letter queues — when to use, how to drain/replay
- [ ] Decoupling — queues/PubSub vs. sync calls; backpressure handling
- [ ] Crash-mid-batch guarantee *(probe)* — checkpoint/watermark resume, transactional batch boundaries, dedup on re-run. *Signal: state the exact mechanism, not "it's idempotent".*
- [ ] Partial failure + alerting — batch statuses, structured alerts

### Q: Slowed-down ETL job diagnosis *(§2.2, Phase 4)*

- [ ] Execution plan / DAG reading — where stage time goes
- [ ] Data skew — stragglers, null-key joins, high-cardinality hot keys
- [ ] Skew fixes — salting, broadcast joins for small tables, skew hints
- [ ] Partition pruning + incremental processing — watermarks, CDC instead of full scans
- [ ] Memory/spill diagnostics — shuffle to disk, executor OOMs
- [ ] Anti-pattern awareness — why "add nodes" is the wrong first answer

### Coding drills (Phase 6)

- [ ] Messy log parsing — malformed-line handling, structured output *(K/A)*
- [ ] Token bucket rate limiter — burst behavior explained *(K)*
- [ ] Merge overlapping intervals — classic; production framing
- [ ] Top-K in an unbounded stream — heap + bounded memory (space-saving)
- [ ] Dedupe-keep-latest + idempotency — the FDE-flavored one
- [ ] Production-code instinct — naming, edge cases, complexity stated unprompted

---

## Section B — Data Modeling & Compute (20% weight)

### Q: Operational entity model (orgs/facilities/equipment/tasks) *(§2.1, Phase 6 SD drill)*

- [ ] Mutable state vs. immutable event log — current view + audit history separation
- [ ] Cardinality handling — many-to-many staff↔facility join tables
- [ ] State machines — task transitions Pending→In-Progress→Completed/Exception
- [ ] Temporal modeling *(probe)* — equipment shared across facilities on alternating weeks → association table with validity windows. *Signal: answer this without denormalizing the base schema.*
- [ ] Query-pattern-driven design — denormalize for hot reads, avoid distributed joins on UI paths
- [ ] Indexing strategy — what you'd index and why

### Q: Two-way writeback console *(§4.1, Phase 4 + SD drill)*

- [ ] Concurrency control — optimistic locking (version stamps, ETags) vs. leases/reservations
- [ ] Idempotent write APIs — safe retries, dedupe request IDs
- [ ] Transactional vs. analytical stores — never write to the lake on a click
- [ ] Optimistic UI + compensating rollback
- [ ] Immutable audit log on every write
- [ ] Race-condition war story — two supervisors, same record *(signal: describe exact conflict resolution)*

---

## Section C — Applied AI, RAG & Agents (15% weight)

### Q: Enterprise assistant over policy docs *(§3.1, Phase 2)*

- [ ] Hybrid search — BM25 + dense vectors; when each wins; fusion (RRF, weighted)
- [ ] Chunking — structure-aware, parent-child; failure modes of too-small vs. too-large
- [ ] Metadata filtering + re-ranking — what a re-ranker buys vs. latency cost
- [ ] Grounding & citation — how you force exact source attribution
- [ ] Abstention — confidence thresholds, deterministic "can't verify" fallback
- [ ] Doc versioning *(probe)* — superseded policies → versioned metadata, atomic re-index/swap, no stale-answer window
- [ ] Sloppy queries — query rewriting, expansion, multi-query retrieval, synonyms

### Q: Vector store choice on GCP *(Phase 2)*

- [ ] Vertex AI Vector Search vs. pgvector vs. BigQuery vector — scale/latency/filtering/ops trade-offs *(probably H — pick one and use it)*

### Q: RAG evaluation *(Phase 2)*

- [ ] Golden eval set from real queries — not synthetic-only
- [ ] Metrics — retrieval recall@k, faithfulness, answer relevance; LLM-as-judge limits
- [ ] Regression gating — eval runs on every prompt/index/model change

### Q: Enterprise vs. academic metrics *(§3.2)*

- [ ] Business KPIs — task time, SLA breaches, $ saved, error rates in real usage
- [ ] HITL telemetry — override rate, copy-paste, thumbs feedback, adoption curves

### Q: Guardrails *(Phase 2)*

- [ ] PII detection/masking on input + output
- [ ] Prompt-injection defenses — instruction hierarchy, tool-output distrust
- [ ] Output validation — schema enforcement, groundedness checks
- [ ] Abuse controls — rate limits, safe defaults on failure

### Q: Agentic systems *(Phase 3)*

- [ ] ReAct loop — when reasoning+acting beats one call; when it's overkill (cost/latency/reliability)
- [ ] Tool design — typed schemas, arg validation, error text fed back to model, retry vs. escalate
- [ ] Runaway guards — max iterations, token/tool budgets, circuit breakers, human checkpoint before irreversible actions
- [ ] **ADK vs. LangGraph** *(likely H — near-zero hands-on)* — agent/tool model + Vertex integration vs. explicit state graphs; pick by fit
- [ ] Multi-agent justification — specialization/context isolation vs. coordination cost; default single-agent
- [ ] Hierarchical orchestrator-worker — who holds the plan, output merge/validation, failure propagation
- [ ] State & memory — checkpointing, session memory, summarization, idempotent crash-resume
- [ ] Agent testing — trajectory evals, tool-call assertions, trace replay, scenario sets (not "ran it, looked right")

### Q: Vertex/Gemini fluency *(Phase 1)*

- [ ] Tokens/context/temperature — explain to non-ML audience with practical consequences
- [ ] Inconsistent output levers, in order — system instructions → few-shot → JSON schema/structured output → temperature → model/fine-tune last
- [ ] Pro vs. Flash per workload — latency/cost/quality routing
- [ ] Vertex AI vs. direct Gemini API — VPC, IAM, eval tooling, Model Garden vs. prototype speed

---

## Section D — Production AI Operations (feeds Production pillar)

### Q: LLM latency / anomaly incidents *(Phase 4, §6.2)*

- [ ] p95 triage — split model vs. retrieval vs. orchestration via traces; token counts, cold starts, quota
- [ ] Fail-safes — circuit breakers, last-known-good cache, rule-based degrade path
- [ ] Escalation — human-in-the-loop queue, on-call alerting; workflow never fully halts
- [ ] AI-specific monitoring — drift, hallucination/override rates, per-request cost, token usage, tool-call success — plus golden signals
- [ ] End-to-end tracing — OpenTelemetry spans per LLM/tool/retrieval call, trace IDs tied to feedback *(likely H)*
- [ ] Eval pipelines in CI — versioned eval sets, automated scoring, thresholds, rollback *(likely H)*
- [ ] Cost reduction — measure breakdown → model routing, caching, prompt compaction, batching, verified by evals
- [ ] Scaling 10→10k users — QPS/quota ceilings, index latency, cache layers, autoscaling, async eval

### Q: Access control end-to-end *(§6.1, Phase 4)*

- [ ] RBAC/ABAC enforced at data + API layers, not just UI
- [ ] Row-level security, masking/tokenization of sensitive fields
- [ ] Least-privilege service accounts — predefined over primitive roles, no SA keys in code/images
- [ ] Secret rotation, audit logs on read/export
- [ ] GCP specifics — how a Cloud Run service reaches private Cloud SQL + Secret Manager *(Phase 1 GCP Q2)*

---

## Section E — Stakeholder, Scoping & Behavioral (40% combined weight)

### Q: Discovery sessions *(§5.1, Phase 5)*

- [ ] "Ask why" before architecture — resist solutioning
- [ ] Shadowing — map the real manual process (chat handoffs, Excel trackers)
- [ ] Problem typing — process vs. data-visibility vs. tooling problem
- [ ] MVP scoping — 2–3 week high-leverage slice
- [ ] "No AI needed" probe — ship the filtered priority list, say so plainly
- [ ] Requirements → architecture — identify the real decisions users make, measurable success metric, phased scope, explicit assumptions

### Q: Communication *(§5.2, §1.3 probe, Phase 5)*

- [ ] Latency/cost/accuracy to a non-engineer — analogies, money/time/risk, zero acronyms
- [ ] Pushing back on a "sexier" solution — anchor on their goals, concrete comparison, no condescension
- [ ] Architecture review facilitation — options-with-trade-offs framing, listen before defending, action items + owners
- [ ] 60-second exec value answer — business metrics first, honest about limits

### Q: Validation UX under time pressure *(§4.2, Phase 5)*

- [ ] Tiered validation — instant client-side format checks + authoritative server-side rules
- [ ] Selective friction — confirmations only for irreversible actions; warnings for low-risk
- [ ] Draft state, undo, human-readable errors
- [ ] Alert-fatigue failure mode — why hard stops push users back to spreadsheets

### Behavioral bank *(§7, Phase 5–6)* — one STAR each:

- [ ] 80%-in-2-weeks ship *(§7.1)* — what you compromised, how you disclosed limits
- [ ] Tool users rejected *(§7.2)* — humility, friction curiosity, modified/discarded code
- [ ] Something you owned broke *(§7.3)* — "I owned it, validation failed here, fixed thus"
- [ ] Ambiguity navigation, conflict, customer obsession, technical leadership, failure+learning — fill the bank to 6–10 stories

---

## Section F — Synthesis Drills (prove the pillars compose)

- [ ] **FDE whiteboard (§8, Phase 6)** — 15-min: ingestion gates → entity model → interactive UI → transactional writeback → governance. Level 3 = full lifecycle + you asked about latency/user constraints.
- [ ] Task-assignment service design *(§2.1 applied)*
- [ ] 50k-doc RAG w/ citations + abstention *(§3.1 applied)*
- [ ] Multi-agent ticket triage — and justify agents vs. simple pipeline
- [ ] Eval + observability layer for an LLM platform *(§6.2 applied)*
- [ ] RAG platform on GCP from memory — every service justified
- [ ] "Isolated to customer VPC, no public egress" — private endpoints, PSC, VPC-SC *(likely K — check your GCP networking depth)*
- [ ] "5 nines on the read path" — what you'd actually promise, where the real risk is

---

## Likely gap shortlist (from your baseline — verify, don't trust)

1. **ADK hands-on** — near-zero today; Phase 3 gate requires a running agent
2. **RAG + Vertex AI implementation** — theory vs. a running pipeline on GCP
3. **LLM observability/eval pipelines** — OpenTelemetry tracing, CI eval gates
4. **GCP networking/ isolation depth** — VPC connector, PSC, VPC-SC for the isolation drills
5. **Discovery reps** — the one skill that needs a live human; do a mock session

## Loop

Weekly: pick the highest-weight ❌ → get the concept explained → rep it out loud
→ log it
→ re-score anything ≤3 the next week.
