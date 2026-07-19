# Healthcare RAG Platform — Overview

**Complexity tier:** Intermediate
**Business Problem:** (fill in — e.g., clinical staff / patients need fast, accurate answers
from large volumes of unstructured healthcare documents — policies, care guidelines, FAQs —
without waiting on a human expert.)

## Why this project

Leverages existing healthcare domain background (DaVita Kidney Care experience) to produce
a credible, differentiated interview narrative — not a generic tutorial clone.

## Scope (v1)

- Ingest a small set of sample clinical/policy documents
- Chunk → embed → store in a vector DB
- Retrieve relevant chunks for a query
- Generate grounded answers via Gemini on Vertex AI

## GCP Services Used

- Vertex AI (embeddings + Gemini generation)
- (Vector store — decide: Vertex AI Vector Search / AlloyDB / other — log decision in decisions.md)
- Cloud Run (serving, once past prototype stage)
- Cloud Storage (source documents)

## AI Components

- Embedding model
- Retrieval strategy (top-k, reranking — TBD)
- Generation / grounding via Gemini
- (Later) Evaluation harness for answer quality

## Stretch Goals

- Add an ADK agent layer on top (e.g., a triage agent that decides which knowledge base to query)
- Multi-document-type support (structured + unstructured)
- Add basic evaluation pipeline (faithfulness, relevance)
- Add observability/tracing

## Interview Relevance

Directly demonstrates: RAG system design, Vertex AI hands-on experience, healthcare domain
credibility, and (once agentic layer is added) agentic system design — all top-priority
FDE interview topics.
