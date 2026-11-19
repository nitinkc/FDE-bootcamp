# Phase 2 — Applied AI Engineering

**Goal:** Build production-grade AI applications.

## Master
- [ ] RAG
- [ ] Embeddings
- [ ] Vector Databases
- [ ] Knowledge Retrieval
- [ ] Enterprise Search
- [ ] Evaluation Frameworks
- [ ] Safety and Guardrails

## Self-Interview Check

Ask each question **cold and out loud** (~2–3 min each). Score honestly:
**1** = couldn't answer · **3** = partial / hand-wavy · **5** = crisp with production depth.
Questions marked §x.x are expanded in the [Interview Deep Dive](#interview-deep-dive) below.

### RAG & Retrieval

1. **"Design an internal assistant that answers questions from thousands of corporate policies, tickets, and runbooks. How do you prevent hallucinations, cite exact sources, and handle questions the docs can't answer?"** *(§3.1)*
   - Strong answer: hybrid search, deliberate chunking, metadata filtering, re-ranking, confidence thresholds with a deterministic "I can't verify this" fallback.
2. **"Walk through your chunking strategy — size, overlap, document structure. What breaks when you get it wrong?"**
   - Strong answer: structure-aware chunking, parent-child retrieval, can describe failure modes of too-small (lost context) and too-large (diluted embeddings) chunks.
3. **"Dense embeddings vs. keyword (BM25) vs. hybrid — when does each win?"**
   - Strong answer: hybrid as enterprise default; keyword for exact IDs/codes/jargon; vector for semantic paraphrase; knows how to fuse (RRF, weighted).
4. **"What does a re-ranker buy you, and what does it cost?"**
   - Strong answer: precision gain on top-k → top-n at the price of added latency; knows when it's worth it.
5. **"A policy document is superseded by a new version. How do you update the index without corrupting retrieval?"** *(§3.1 probe)*
   - Strong answer: document versioning metadata, atomic re-embed/swap, invalidation strategy, no stale-answer window.

### Vector Databases & Enterprise Search

1. **"Which vector store do you pick on GCP — Vertex AI Vector Search, pgvector (AlloyDB/Cloud SQL), BigQuery vector — and why?"**
   - Strong answer: reasons from scale, latency, filtering needs, and ops burden — not just a brand name.
2. **"Users type short, sloppy queries ('that form for the thing'). How do you still find the right document?"**
   - Strong answer: query rewriting/expansion, multi-query retrieval, synonyms, feedback loops.

### Evaluation & Safety

1. **"How do you evaluate a RAG system? What's in your eval set and which metrics do you track?"**
   - Strong answer: a golden Q&A set from real user queries, retrieval recall + faithfulness + answer relevance, regression gate on every change.
2. **"Academia measures F1. How do you prove an enterprise AI tool actually adds value?"** *(§3.2)*
   - Strong answer: task completion time, SLA breaches, error rates in real usage, user override/thumbs-down telemetry, adoption.
3. **"What guardrails does a production LLM app need — on inputs, outputs, and abuse?"**
    - Strong answer: PII handling, prompt-injection defenses, output schema/grounding validation, rate limits, safe defaults on failure.

### Phase Gate

- [ ] Scored **4+ on ≥80%** of the questions above, out loud, without notes.
- [ ] Can whiteboard a full RAG architecture (ingest → index → retrieve → generate → eval) in under 10 minutes.

## Interview Deep Dive

*Full interviewer context for the §-marked questions above — what's actually being tested.*

### §3.1 — Deploying Practical Retrieval & Automation Systems (RAG / Search / Agents)

- **Question:** "If you are building an internal search or automated assistant for operational teams who need accurate answers from thousands of corporate policies, tickets, and operational guidelines, how do you design the system to prevent hallucinations, cite exact sources, and gracefully handle queries where the data does not exist?"
- **Good signs:** hybrid search (BM25 keyword + dense vector embeddings); deliberate chunking strategies, metadata filtering, re-ranking; confidence scoring thresholds with deterministic fallback responses (e.g., "I cannot verify this in policy documentation") rather than guessing.
- **Red flags:** believes an off-the-shelf vector database with default naive chunking and basic prompt engineering is ready for mission-critical enterprise deployment.
- **Follow-up probe:** "How do you handle policy documents that supersede older versions without corrupting the retrieval index?"

### §3.2 — Defining Enterprise Success vs. Academic Metrics

- **Question:** "In academia, success is measured by benchmark metrics like accuracy, F1-score, or loss curves. In an enterprise role, how do you define and measure whether an automated workflow tool is actually successful and adding value to users?"
- **Good signs:** connects system performance to business operational metrics — human task completion time, SLA breach reduction, dollar savings, error rates in active usage; establishes human-in-the-loop telemetry (user override rates, copy-paste activity, thumbs-up/down feedback loops).
- **Red flags:** fixates solely on mathematical loss curves or validation metrics; does not consider whether users actually adopt the software.

## Notes / Evidence
