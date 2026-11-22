# Lesson 11 — Interview Readiness

*Phase 6 · The self-interview method, drills, and scoring.*

## What Interviewers Evaluate (the 4 pillars)

1. **Production systems & code** — APIs, CI/CD, testing, scale.
2. **Data modeling & architecture** — pipelines, state, sync.
3. **Forward deployment & discovery** — root cause, user workflow, UI.
4. **Governance & security** — RBAC/ABAC, audit, fail-safes.

Across all of them: engineering hygiene over academic metrics, decompose
ambiguous problems, pragmatic velocity (80% in weeks), stakeholder translation,
end-to-end ownership.

## How to Self-Interview

1. **Answer out loud, cold** — no notes; interviews are verbal.
2. **Timebox:** ~2 min/knowledge question, 15 min/whiteboard, 3 min/behavioral
   (STAR).
3. **Score 1–5 honestly** — 5 = crisp with production depth + follow-up depth.
4. **Log every session;** re-ask anything ≤3 next week.
5. Feed the scorecard into your Interview %.

## Drill Inventory

- **Coding (45 min, no AI assist):** parse messy logs without crashing; token
  bucket rate limiter; merge overlapping windows; top-K in a stream; idempotent
  dedupe by timestamp. *They probe complexity, edge cases, and whether your code
  looks like production code.*
- **System design (15–20 min):** task-assignment service; ingestion across
  unreliable sources (1.2); idempotent writeback API (4.1).
- **AI system design:** 50k-doc assistant with citations + fallback (3.1);
  multi-agent ticket triage — justify agents vs. a pipeline; eval +
  observability layer (6.2).
- **GCP architecture:** rebuild the Healthcare RAG platform from memory;
  VPC-isolated design with no public egress; "5 nines on the read path."

## The FDE Whiteboard (signature drill, 15 min)

1,000 branch offices on disconnected spreadsheets → design: **ingestion with
validation gates + DLQ → cleansed core data layer → operational entity model →
coordinator UI + automated risk engine → audited writeback to enterprise
systems.**

Rubric: Level 1 builds only an ML model. Level 2 builds read-only ETL +
dashboard. **Level 3 (hire):** covers the full lifecycle — ingestion validation,
entity model, interactive app, transactional writeback, access governance — and
*asks about latency requirements and operational constraints first.*

## Scorecard

Weighted pillars: Production Engineering 25% · Data Modeling 20% · Pragmatism &
Applied AI 15% · Stakeholder & Scoping 20% · Accountability & GSD 20%.

- <50% not ready · 50–70% drill weakest pillars · 70–85% timed mocks ·
  85%+ schedule real interviews.
