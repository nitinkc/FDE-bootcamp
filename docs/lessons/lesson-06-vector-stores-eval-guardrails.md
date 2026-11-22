# Lesson 06 — Vector Stores, Evaluation & Guardrails

*Phase 2 · Vector DB & Eval/Safety questions + deep dive 3.2.*

## Choosing a Vector Store on GCP

Reason from scale, latency, filtering, and ops burden — not brand names:

- **Vertex AI Vector Search** — purpose-built, massive scale, low-latency ANN;
  managed but another service to operate.
- **pgvector (Cloud SQL / AlloyDB)** — vectors live beside your relational
  data; simple ops, easy metadata joins; best at moderate scale.
- **BigQuery vector search** — vectors colocated with analytics; great when the
  corpus already lives in BQ and latency requirements are relaxed.

## Sloppy Short Queries ("that form for the thing")

- **Query rewriting/expansion** — LLM rewrites the query, adds synonyms.
- **Multi-query retrieval** — generate variants, retrieve for each, merge.
- **Synonym/acronym maps** — domain vocabulary matters.
- **Feedback loop** — log clicks/thumbs-down to improve over time.

## Evaluating a RAG System

- **Golden eval set** — real user questions with known-good answers/sources.
- **Metrics:** retrieval recall (did we fetch the right chunks?), faithfulness
  (answer grounded in sources?), answer relevance.
- **Regression gate** — eval runs on every prompt/model/retrieval change.

## Enterprise Success ≠ Academic Metrics (3.2)

F1 and loss curves don't prove value. Measure:

- Task completion time, SLA breach reduction, error rates in real usage.
- **Human-in-the-loop telemetry** — override rates, thumbs up/down, copy-paste
  activity.
- **Adoption** — do people actually use it?

## Production Guardrails

- **Inputs:** PII detection/handling, prompt-injection defenses, input length
  and content limits.
- **Outputs:** schema/grounding validation before showing users; safe default
  (fallback message) when validation fails.
- **Abuse:** rate limits, auth, audit logging.
