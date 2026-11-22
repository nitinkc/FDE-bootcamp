# Lesson 05 — RAG & Retrieval

*Phase 2 · RAG & Retrieval questions + deep dive 3.1.*

## The Architecture (whiteboard in <10 min)

`ingest → chunk → embed → index → retrieve → re-rank → generate → cite → eval`

**Enterprise assistant over policies/runbooks — how to prevent hallucination:**

- **Hybrid search** — keyword (BM25) + dense vectors.
- **Deliberate chunking** + **metadata filtering** (doc type, version, dept).
- **Re-ranking** top-k → top-n.
- **Citations** — every claim linked to a source chunk.
- **Confidence threshold + deterministic fallback** — "I can't verify this in
  policy documentation" instead of guessing.
- **Red flag:** "vector DB + default chunking + a prompt" = not production-ready.

## Chunking

- **Structure-aware** — split on headings/sections, keep tables/lists intact;
  attach metadata (title, path, version).
- **Parent-child retrieval** — embed small chunks, return the parent section.
- **Failure modes:** too small → context lost, fragmented answers; too large →
  diluted embeddings, noisy retrieval, wasted context window.

## Dense vs Keyword vs Hybrid

- **BM25/keyword wins:** exact IDs, codes, jargon, part numbers.
- **Dense vectors win:** paraphrases, conceptual questions, sloppy phrasing.
- **Hybrid is the enterprise default** — fuse with RRF (reciprocal rank fusion)
  or weighted scores.

## Re-ranking

- Cross-encoder over top-k gives a real precision bump on the final top-n.
- **Cost:** added latency on every query — apply to the top-k only, and skip it
  where latency is tight and recall is already good.

## Index Updates When Docs Are Superseded

- **Version metadata** on every chunk; retrieval filters to current versions.
- **Atomic swap** — re-embed + replace as one operation; never a window where
  old and new chunks coexist as equals.
- **Invalidation path** — deletes/deprecations propagate to the index, not just
  the doc store.
