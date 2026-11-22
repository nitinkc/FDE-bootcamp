# Phase 6 — Interview Readiness

**This is the master self-interview doc.** It combines the full roadmap's
interview material in one place to learn, test yourself, and measure how
ready you actually are.

## What Interviewers Evaluate

An FDE operates at the tip of the spear: embedded with operational teams and
business leadership, turning messy real-world bottlenecks into data pipelines,
entity models, and production workflows people rely on daily. Technical
brilliance in a sandbox is table stakes — the real hiring filter is engineering
hygiene, pragmatic velocity, and operational empathy.

```text
                           ┌──────────────────────────────────────────────┐
                           │               The Modern FDE                 │
                           │     Bridging Enterprise Tech & Business      │
                           └──────────────────────┬───────────────────────┘
                                                  │
         ┌────────────────────────┬───────────────┴───────────────┬────────────────────────┐
         ▼                        ▼                               ▼                        ▼
┌──────────────────┐    ┌──────────────────┐            ┌──────────────────┐    ┌──────────────────┐
│  1. Production   │    │ 2. Data Modeling │            │ 3. Forward       │    │ 4. Governance &  │
│  Systems & Code  │    │  & Architecture  │            │  Deployment &    │    │  Security        │
│  (APIs, CI/CD,   │    │ (Pipelines,      │            │  Discovery       │    │  (RBAC/ABAC,     │
│  Testing, Scale) │    │  State, Sync)    │            │ (Root Cause, UI) │    │  Audit, Failsafe)│
└──────────────────┘    └──────────────────┘            └──────────────────┘    └──────────────────┘
```

Key focus areas:

- **Academic rigor vs. engineering delivery** — modular, deployable, testable code over single-run notebooks.
- **Ambiguous problem solving** — deconstruct ill-defined operational pain points into phased, scoped architectures.
- **Pragmatism & speed (GSD)** — ship a high-value 80% solution in weeks and iterate, no perfectionist paralysis.
- **Stakeholder translation** — communicate trade-offs to non-technical partners without jargon or condescension.
- **End-to-end ownership** — extreme accountability for uptime, user adoption, and data accuracy.

## How to Self-Interview

1. **Answer out loud, cold.** No notes, no re-reads. Real interviews are verbal —
   thinking silently doesn't count.
2. **Timebox.** ~2 min per knowledge question, 15 min per whiteboard prompt,
   3 min per behavioral story (STAR).
3. **Score honestly.** 1 = couldn't answer · 2 = vague/guessed · 3 = partial ·
   4 = solid with minor gaps · 5 = crisp with production depth and follow-up depth.
4. **Log every session and every drill.**
   Re-ask anything scored ≤3 the following week.
5. **Feed the scorecard** below into your Interview % on the [home page](../index.md).

## Question Banks by Phase

Work the Self-Interview Check in each phase — those are the core knowledge questions:

| Phase | Focus | Question Bank |
| --- | --- | --- |
| 1 — Foundation | Production code hygiene, GCP core, LLM/Vertex basics | [Phase 1 check](phase-1-foundation.md#self-interview-check) |
| 2 — Applied AI | RAG, retrieval, eval, guardrails | [Phase 2 check](phase-2-applied-ai.md#self-interview-check) |
| 3 — Agentic | ReAct, ADK/LangGraph, tool use, state | [Phase 3 check](phase-3-agentic-systems.md#self-interview-check) |
| 4 — Production AI | Observability, eval pipelines, cost, security, writebacks | [Phase 4 check](phase-4-production-ai.md#self-interview-check) |
| 5 — FDE Excellence | Discovery, exec comms, ownership stories | [Phase 5 check](phase-5-fde-excellence.md#self-interview-check) |

## Coding

- [ ] Python
- [ ] Problem Solving
- [ ] Data Structures
- [ ] Algorithms

**Drill prompts** (45 min each, real editor, no AI assist):

1. Parse a messy log file into structured records; handle malformed lines without crashing.
2. Implement a rate limiter (token bucket) — then explain how it behaves under burst.
3. Merge overlapping maintenance windows from two systems into one schedule.
4. Find the top-K most frequent error codes in a stream too big for memory.
5. Dedupe records keeping the most recent version by timestamp — then make it idempotent.

*Interviewers probe: complexity, edge cases, and whether your code looks like production code or a notebook script.*

## System Design

- [ ] Traditional System Design
- [ ] API Design
- [ ] Distributed Systems

**Drill prompts** (15–20 min whiteboard each):

1. Design a task-assignment service for field operators (entities, state transitions, audit).
2. Design an ingestion pipeline across unreliable legacy sources — schema drift, retries, DLQs. *(1.2)*
3. Design an idempotent writeback API for an Approve/Reject console. *(4.1)*

## AI System Design

- [ ] RAG Systems
- [ ] Agentic Systems
- [ ] Enterprise AI Platforms

**Drill prompts:**

1. Design an enterprise assistant over 50k policy docs with citations and zero-hallucination fallbacks. *(3.1)*
2. Design a multi-agent workflow that triages ops tickets — justify why agents vs. a simple pipeline.
3. Design the eval + observability layer for a production LLM platform. *(6.2)*

## The FDE Whiteboard Scenario

The signature drill (8) — time yourself to **15 minutes**:

> *1,000 branch offices log equipment maintenance, tasks, and supplies in
> disconnected spreadsheets, causing stockouts and delayed maintenance.
> Design an end-to-end system that (1) ingests branch + central data,
> (2) gives a unified operational view of branch health and inventory risk,
> (3) lets regional coordinators reallocate supplies and dispatch technicians,
> (4) writes back to enterprise systems with full auditability.*

Target shape:

```text
                             [Branch & Central Sources]
                                         │
                                         ▼
                            [Ingestion & Ingestion Gates]
                            (Schema Validation, DLQ, CDC)
                                         │
                                         ▼
                            [Core Data Layer / Transforms]
                            (Incrementalization & Cleansing)
                                         │
                                         ▼
                             [Operational Entity Model]
                         (Branch, Supply, Tech, Assignment)
                                         │
                    ┌────────────────────┴────────────────────┐
                    ▼                                         ▼
      [Interactive Coordinator UI]                [Automated Risk Engine]
                    │                                         │
                    ▼                                         │
      [Action Dispatch / Writeback] ◄─────────────────────────┘
      (Optimistic Locking, Audit)
                    │
                    ▼
      [Target Enterprise Systems]
```

**Full interviewer rubric:**

- **Level 1 (Junior/Pure Research):** Focuses solely on an ML model to predict
  supply demand; ignores ingestion failures, concurrency, writebacks, and user
  workflow design.
- **Level 2 (Standard Engineer):** Designs a clean batch ETL pipeline and a
  passive read-only dashboard; struggles when pressed on two-way action
  writeback, optimistic locking, or role-based security.
- **Level 3 (Strong FDE Hire):** Maps the complete data lifecycle — ingestion
  validation, entity relationships, interactive user application, transactional
  writeback, and access governance. Proactively asks about data latency
  requirements and user operational constraints.

## GCP Architecture

- [ ] Cloud Design
- [ ] Security
- [ ] Scalability
- [ ] Reliability

**Drill prompts:**

1. Architect the Healthcare RAG Platform on GCP from memory — every service justified.
2. "A customer needs this app isolated to their VPC with no public egress." Design it.
3. "Design for 5 nines on the read path." What do you actually promise, and where's the real risk?

## Behavioral Interviews

- [ ] Leadership
- [ ] Conflict Resolution
- [ ] Ownership
- [ ] Customer Obsession
- [ ] Ambiguity Navigation

Every competency needs a STAR story in the [story bank](../interview-prep/behavioral-stories.md),
plus these FDE-specific prompts (7 — deep dive in Phase 5):

- "A time you shipped an 80% solution in two weeks instead of perfecting it — what did you compromise?" *(7.1)*
- "A tool you built that users rejected — what did you do?" *(7.2)*
- "Something you owned went wrong — how did you communicate and fix it?" *(7.3)*

## Self-Score Scorecard

After a round of question banks + one whiteboard + behavioral, score each pillar
1–5 and weight it — adapted from the interviewer's scorecard (9):

| Competency Pillar | Weight | You're a 5 when you… | Score (1–5) |
| --- | --- | --- | --- |
| Production Engineering | 25% | Have shipped production services; testing, Docker, resilience, clean API contracts are reflexes | |
| Data Modeling & Compute | 20% | Model entity relationships cleanly; diagnose skew, partitions, execution plans | |
| Pragmatism & Applied AI | 15% | Pick the simplest robust solution; measure business value, not loss curves | |
| Stakeholder & Scoping | 20% | Shadow users, find root bottlenecks, translate trade-offs into business risk | |
| Accountability & GSD | 20% | Ship 80% MVPs to learn; own failures fully; measure success by adoption | |

**Weighted readiness = Σ(pillar × weight) / 5 → Interview %.**

| Weighted score | Verdict |
| --- | --- |
| < 50% | Not ready — keep building, revisit the weakest phase's question bank |
| 50–70% | Getting there — drill your two lowest pillars weekly |
| 70–85% | Interview-capable — start timed full mocks |
| 85%+ | Ready — schedule real interviews |

### Interviewer Rubric (9)

The full scoring grid an interviewer uses — same pillars, with what each level
looks like:

| Competency Pillar | Weight | Level 1 (Definite No-Hire) | Level 3 (Borderline / Trainable) | Level 5 (Strong FDE Hire) |
| --- | --- | --- | --- | --- |
| **Production Engineering** | 25% | Only ad-hoc scripts in local notebooks; no awareness of testing or CI/CD | Understands engineering hygiene; has built APIs but lacks production scale or telemetry | Has shipped production services; automated testing, Docker, resilience, clean API contracts are reflexes |
| **Data Modeling & Compute** | 20% | Flattens everything into unmanageable flat files; suggests hardware to fix slow queries | Understands normalization and basic indexing; needs guidance on data skew and incremental builds | Models complex entity relationships cleanly; diagnoses skew, partition pruning, execution DAGs |
| **Pragmatism & Applied AI** | 15% | Always insists on the most complex, cutting-edge architecture; optimizes for academic metrics | Can implement RAG and ML baselines; occasionally over-engineers before checking simple alternatives | Instinctively picks the simplest robust solution; sets clear business-value metrics and human fallback loops |
| **Stakeholder & Scoping** | 20% | Dense technical jargon; expects polished specs before writing code | Communicates adequately; translates technical ideas if prompted; focuses on the tech, not the problem | Deeply empathetic; shadows users to find root bottlenecks; translates trade-offs into business risk |
| **Accountability & GSD** | 20% | Perfectionist paralysis; blames teammates, bad data, or users when software fails | Iterates quickly but gets uncomfortable when requirements shift | Extreme ownership; comfortable shipping 80% MVPs to learn; humble, accountable, measures success by adoption |

