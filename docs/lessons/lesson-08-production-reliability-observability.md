# Lesson 08 — Production AI: Reliability & Observability

*Phase 4 · Reliability & Debugging, Observability & Eval questions + 2.2, 6.2.*

## Diagnosing a Slowed-Down Job (25 min → 4 hrs)

Systematic, in this order:

1. **Execution plan / DAG** — which stage got slower?
2. **Stage timings & I/O wait, memory allocation.**
3. **Data skew** — null keys or hot values stranding one worker while others
   finish.
4. **Fixes:** broadcast joins for small lookups, salting skewed keys, partition
   pruning, converting full scans to **watermark-based incremental** loads.
- **Red flag:** "add more nodes/RAM" before inspecting plans.

## LLM Endpoint p95 Tripled Overnight

- **Split the latency** via traces: model time vs retrieval vs orchestration.
- Check **token counts** (longer prompts/responses?), **cold starts**, upstream
  dependency changes, new deployments.

## AI-Specific Monitoring

Beyond the usual golden signals (latency, errors, saturation):

- **Quality/eval metrics** over time, **drift**.
- **Hallucination / user-override rates.**
- **Per-request cost, token usage.**
- **Tool-call success rates** for agents.

## Eval Pipeline as a Ship Gate

- **Versioned eval sets**, automated scoring in CI, pass/fail thresholds.
- Human spot-checks on samples; **rollback path** when evals regress.
- Gates *every* change: prompt, model, retrieval config.

## End-to-End Tracing

- **OpenTelemetry spans** per LLM call, tool call, and retrieval step.
- Trace IDs linked to user feedback; per-span latency and cost attribution.

## Fail-Safes & Safe Defaults (6.2)

When automation fails at 2 a.m., the frontline keeps working:

- **Circuit breakers** — pause automated actions when anomaly rates cross a
  threshold.
- **Graceful degradation** — rule-based defaults or last-known-good cached
  data.
- **Human escalation queue** + instant on-call notification.
- **Red flag:** believing "high availability = code never fails." Plan for
  *partial* failure.
