# Phase 3 — Agentic Systems

**Goal:** Build sophisticated agent workflows similar to those expected in modern enterprise AI deployments.

## Master
- [ ] LangGraph (secondary/comparative)
- [ ] ADK (priority)
- [ ] ReAct
- [ ] Tool Use
- [ ] Agent Planning
- [ ] Multi-Agent Architectures
- [ ] State Management

## Self-Interview Check

Ask each question **cold and out loud** (~2–3 min each). Score honestly:
**1** = couldn't answer · **3** = partial / hand-wavy · **5** = crisp with production depth.
Cross-references like §5.1 point to deep dives in the other phase docs.

### Core Patterns

1. **"Explain the ReAct loop. When does reasoning + acting beat a single well-prompted LLM call — and when is it overkill?"**
   - Strong answer: multi-step tasks needing observations between steps; honestly states a fixed chain or single call often wins on cost, latency, and reliability.
2. **"Design a tool-using agent that looks up operational data via an API. How do you define the tools, validate calls, and handle tool failures?"**
   - Strong answer: tight typed tool schemas, argument validation, retry vs. escalate decisions, clear error messages fed back to the model.
3. **"What stops an agent from looping forever, spiraling on tool errors, or burning budget?"**
   - Strong answer: max iterations, tool-call/token budgets, circuit breakers, human checkpoints before irreversible actions.

### Frameworks & Architecture

1. **"How do ADK and LangGraph each model agents and control flow? Which would you pick for a GCP deployment and why?"**
   - Strong answer: honest comparison — ADK's agent/tool model + Vertex integration vs. LangGraph's explicit state graphs; picks based on fit, not hype.
2. **"When is a multi-agent system justified over one agent with more tools?"**
   - Strong answer: specialization, context isolation, parallel work — weighed against coordination cost, debuggability, and latency. Default stays single-agent.
3. **"Walk through a hierarchical/orchestrator-worker agent design for a real task. Who holds the plan? How do results merge?"**
   - Strong answer: clear division of planning vs. execution, how sub-agent outputs are validated/merged, failure propagation.

### State, Memory & Testing

1. **"How do you manage state and memory across a long-running, multi-step agent task — including resume after a crash?"**
   - Strong answer: checkpointing/persisted state, session memory, summarization for long contexts, idempotent resumption.
2. **"How do you test and evaluate a non-deterministic agentic workflow?"**
   - Strong answer: trajectory evals, assertions on tool calls and outcomes, trace replay, scenario eval sets — not just "ran it and looked right".
3. **"An ops director says: 'build me an AI agent to fix our task handoffs.' What do you verify before writing any agent code?"** *(see Phase 5, §5.1)*
   - Strong answer: discovery first — the fix might be a filtered list, not an agent; only builds agentics after validating a multi-step reasoning need.

### Phase Gate

- [ ] Scored **4+ on ≥80%** of the questions above, out loud, without notes.
- [ ] First ADK agent running.

## Notes / Evidence
