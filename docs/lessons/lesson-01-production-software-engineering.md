# Lesson 01 — Production Software Engineering

*Phase 1 · Prepares you for the Software Engineering questions + deep dive 1.1.*

## Prototype → Production Service

Research code optimizes for a result; production code optimizes for other
people's ability to run, change, and trust it. The transformation:

- **Modular design** — separate domain logic from I/O and config; small modules
  with clear responsibilities, not one notebook-turned-script.
- **API structure** — typed request/response contracts, versioned endpoints,
  consistent error shapes.
- **Error handling** — explicit exception boundaries; failures return useful
  messages, never silent or raw stack traces to users.
- **Containerization** — Docker for reproducible environments.
- **CI/CD** — tests + lint + build on every change; deploy is a pipeline, not a
  manual step.
- **Structured logging & telemetry** — logs with context (request IDs, levels),
  metrics, traces. "Print statements" don't count.
- **Dependency management** — pinned versions, lockfile, no `pip install` at
  runtime.

**The 24-hour handover test:** if you left tomorrow, a new engineer should be
able to run the service from a README/runbook alone — typed interfaces, tests
that document behavior, no tribal knowledge.

## Testing Strategy

Risk-based, not coverage-maximal:

- **Unit tests** — business logic, edge cases, transformations.
- **Integration/contract tests** — boundaries: DB, external APIs, queues. These
  catch what unit tests can't.
- **Don't test** — trivial glue, third-party behavior.
- A bug fix isn't done until it has a **regression test**.

## Debugging Production Issues (can't repro locally)

1. **Observe first** — logs, traces, metrics; don't guess.
2. **Narrow** — bisect recent deploys and config changes; compare working vs.
   broken environment.
3. **Reproduce** — in staging with production-like data/inputs.
4. **Fix + regression test**, then ship.

## Interview signals

- **Good:** hygiene is reflexive — testing, CI, telemetry, clean contracts.
- **Red flag:** treats the code as a one-off artifact; testing "later".
