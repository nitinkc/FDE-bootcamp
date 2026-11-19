# Phase 1 — Foundation

**Goal:** Build confidence as a cloud-native engineer with AI awareness.

## Master

### Software Engineering
- [ ] Python for Production
- [ ] Clean Code
- [ ] Testing
- [ ] Debugging

### GCP
- [ ] Core Services
- [ ] Architecture Patterns
- [ ] Networking
- [ ] Security

### AI Foundations
- [ ] LLM Fundamentals
- [ ] Prompt Engineering
- [ ] Vertex AI Foundations
- [ ] Gemini Ecosystem

## Self-Interview Check

Ask yourself each question **cold and out loud** (~2 min each), as if an interviewer
just asked it. Score yourself honestly:
**1** = couldn't answer · **3** = partial / hand-wavy · **5** = crisp with production depth.

Log scores in your notes as you go. Questions marked §x.x are expanded in the
[Interview Deep Dive](#interview-deep-dive) below.

### Software Engineering Questions

1. **"Walk me through a time you took exploratory code (a notebook or script) and turned it into a real, maintainable service. How did you structure the API, tests, and error handling?"** *(§1.1)*
   - Strong answer: modular design, unit + integration tests, containerization, CI/CD, structured logging, dependency management — not a one-off artifact.
2. **"If another engineer had to take over your last service within 24 hours, what would their onboarding look like?"** *(§1.1 probe)*
   - Strong answer: README/runbook, typed interfaces, tests as documentation, no tribal knowledge.
3. **"How do you decide what to test — unit vs. integration vs. not at all?"**
   - Strong answer: risk-based coverage, contract/boundary tests, doesn't chase 100% for its own sake.
4. **"A bug appears in production that you can't reproduce locally. Walk through your debugging process."**
   - Strong answer: logs/traces/metrics first, bisect deploys & config changes, staging repro, fix + regression test.

### GCP Questions

1. **"Deploy an internal HTTP API on GCP. Which compute do you pick — Cloud Run, GKE, or GCE — and why?"**
   - Strong answer: Cloud Run default for stateless/bursty services, names real trade-offs (cold starts, VPC access, control) rather than reciting features.
2. **"How does a Cloud Run service securely reach a private Cloud SQL instance and a database password?"**
   - Strong answer: VPC connector / private IP, Secret Manager, dedicated service account with least-privilege IAM.
3. **"When do you put Pub/Sub between two services instead of calling directly over HTTP?"**
   - Strong answer: decoupling, retries/backpressure, fan-out, async work — and admits the added operational complexity.
4. **"Explain least-privilege IAM in practice: service accounts, roles, and things you'd never do."**
   - Strong answer: per-service SAs, predefined over primitive roles, no SA key files in code or images, audit logging.

### AI Foundations Questions

1. **"Explain tokens, context window, and temperature to a smart colleague with no ML background."**
   - Strong answer: correct, jargon-free, and connects each concept to a practical consequence (cost, truncation, determinism).
2. **"A Gemini prompt returns inconsistent, badly formatted answers. What levers do you pull, in what order?"**
    - Strong answer: system instructions → few-shot examples → structured output/JSON schema → temperature → only then model or fine-tuning changes.
3. **"Gemini Pro-tier vs Flash-tier models — how do you choose per workload?"**
    - Strong answer: latency/cost/quality trade-off; route easy queries down-tier, hard queries up-tier; measure, don't guess.
4. **"When would you go through Vertex AI vs. calling the Gemini API directly?"**
    - Strong answer: enterprise needs — VPC/private networking, IAM governance, eval tooling, Model Garden/custom tuning vs. fastest path to a prototype.

### Phase Gate

- [ ] Scored **4+ on ≥80%** of the questions above, out loud, without notes.

## Interview Deep Dive

*Full interviewer context for the §-marked questions above — what's actually being tested.*

### §1.1 — Research Prototype to Production Service

*Goal: can you build reliable, maintainable software, or is your experience limited to sandbox scripts and research notebooks?*

- **Question:** "PhD and research projects often optimize for a paper, presentation, or proof-of-concept. Walk me through a time you took code from an exploratory notebook/sandbox and deployed it as a real, usable service. How did you structure the APIs, write tests, handle exceptions, and ensure it was maintainable by others?"
- **Good signs:** modular architecture, automated testing (unit/integration), containerization (Docker), CI/CD pipelines, latency considerations, dependency management, structured logging/telemetry.
- **Red flags:** treats code as a one-off execution artifact; views engineering hygiene, error handling, or testing as an afterthought.
- **Follow-up probe:** "If another engineer had to take over that service within 24 hours of you leaving, what would their onboarding experience have been like?"

### §1.2 — System Design with Imperfect, Distributed Data

- **Question:** "In enterprise environments, data rarely comes neatly packaged like research benchmark datasets. How would you design a data ingestion and processing pipeline that must handle schema changes, missing values, rate limits, and network dropouts across multiple backend legacy systems?"
- **Good signs:** resilience, idempotency, data validation boundaries (e.g., Pydantic/type checks), decoupling via queues or event-driven patterns, dead-letter queues (DLQs), structured alerting.
- **Red flags:** assumes upstream sources will always be clean and well-documented; no strategies for retries, backpressure, or partial batch failures.
- **Follow-up probe:** "How do you guarantee that if a pipeline crashes midway through a 10-million-row batch, re-running it does not duplicate transactional records downstream?"

### §1.3 — Pragmatic Technology Choices (Avoiding Over-Engineering)

- **Question:** "Tell me about a time you had to solve a challenging technical problem and deliberately chose a simple, lightweight approach (a rule-based heuristic, indexed relational lookup, or SQL transform) instead of a complex model or cutting-edge architecture. How did you make that trade-off?"
- **Good signs:** values simplicity, low latency, maintainability, and compute cost; acknowledges the newest model or framework is often the wrong tool for high-stakes operational workflows.
- **Red flags:** insists on cutting-edge research algorithms for problems easily solved by clear business logic or standard indexing.
- **Follow-up probe:** "How did you justify that choice to technical peers who wanted the sexier, more complex tool?"

### §2.1 — Entity & Relationship Modeling (The Operational Ontology)

- **Question:** "You are designing the data model for a national field-operations system involving Organizations, Physical Facilities, Operators, Equipment, and Scheduled Tasks. Operations requires tracking real-time equipment status, reassigning tasks dynamically across staff, and maintaining a historical audit of who performed what action. How would you structure these entities, keys, and relationships?"
- **Good signs:** clean distinction between mutable operational state (current view) and immutable event logs (audit history); thoughtful cardinality (many-to-many staff-to-facility mappings) and task state transitions (`Pending → In-Progress → Completed / Exception`); designs for downstream query patterns to avoid expensive multi-table joins on high-frequency screens.
- **Red flags:** flattens everything into a single massive denormalized table, or designs an academic 5th-normal-form schema that is impossible to query performantly.
- **Follow-up probe:** "How would your model handle equipment that must suddenly be shared across multiple facilities on alternating weeks without rewriting existing reporting queries?"

## Notes / Evidence

Add dated notes and evidence as you complete items.
