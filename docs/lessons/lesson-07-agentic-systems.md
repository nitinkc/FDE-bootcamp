# Lesson 07 — Agentic Systems

*Phase 3 · All Core/Architecture/State questions.*

## ReAct Loop

`Reason → Act (tool call) → Observe → repeat` until the task is done.

- **Worth it:** multi-step tasks where each step depends on the previous
  observation (look up → decide → look up again).
- **Overkill:** fixed-sequence tasks — a deterministic chain or single
  well-prompted call wins on cost, latency, and reliability. Say so honestly.

## Tool-Using Agents

- **Tool schemas:** tight, typed definitions — the model calls what it can
  understand.
- **Validate arguments** before executing; never trust model-generated params
  blindly.
- **Failure handling:** retry transient errors, escalate permanent ones; return
  **clear error messages back to the model** so it can recover or reroute.

## Keeping Agents Under Control

- **Max iterations** and **token/tool-call budgets**.
- **Circuit breakers** on repeated tool failures.
- **Human checkpoint** before irreversible actions (writes, deletes, sends).

## ADK vs LangGraph

- **ADK (Google):** agent/tool abstractions, first-class Vertex AI integration —
  natural fit on GCP.
- **LangGraph:** explicit state graphs — nodes/edges, fine-grained control flow,
  checkpointing; framework-agnostic.
- Pick on fit (deployment target, control model), not hype.

## Multi-Agent vs Single Agent

- **Justify multi-agent by:** specialization, context isolation, parallel work.
- **Costs:** coordination complexity, debugging difficulty, latency.
- **Default is single agent with more tools** — split only when forced.
- **Orchestrator-worker:** orchestrator owns the plan and merges/validates
  worker outputs; define how failures propagate up.

## State & Memory

- **Checkpointing/persisted state** — resume after crash, idempotent resumption.
- **Session memory** for multi-turn; **summarization** when context grows long.

## Evaluating Non-Deterministic Agents

- **Trajectory evals** — assert on the tool calls made and outcomes reached,
  not just final text.
- **Trace replay** — reproduce runs from recorded traces.
- **Scenario eval sets** — known tasks with expected tool sequences/outcomes.
- "Ran it once and it looked right" is not testing.

## Before Building Any Agent

"Build me an AI agent to fix handoffs" → **discovery first** (see Lesson 10).
The fix might be a filtered list. Only build agentics after validating a real
multi-step reasoning need.
