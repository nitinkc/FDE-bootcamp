# Lesson 10 — FDE Excellence

*Phase 5 · Discovery, Communication, Ownership questions + 4.2, 5.1, 5.2, 7.1–7.3.*

## Discovery on Vague Requests (5.1)

"Build me an AI tool for task handoffs" — first two sessions:

1. **Ask "why" repeatedly** before proposing architecture.
2. **Shadow operators** — map the real manual process: informal handoffs,
   side spreadsheets, workarounds.
3. **Classify the problem** — is it a *process* problem, a *data visibility*
   problem, or a *tooling* problem?
4. Land a **focused MVP in 2–3 weeks**.

**The twist:** if discovery shows they don't need AI — just a filtered daily
priority list — **ship that and say so plainly.** The win is solving the
problem, not using AI.

## Translating Vague → Scoped

"Make our reporting smarter" → identify the actual decisions users make →
define a **measurable success metric** → phase the scope → state assumptions
explicitly.

## Designing for Human Error (4.2)

Operators under time pressure — catch errors without alert fatigue:

- **Tiered validation** — instant client-side format checks + authoritative
  server-side business rules.
- **Selective friction** — confirmation modals/reason codes only on
  *irreversible* actions; non-blocking warnings for low-risk anomalies.
- **Draft saving, undo, human-readable errors.**
- **Red flag:** hard stops on everything → users flee back to spreadsheets.

## Communicating to Non-Engineers (5.2)

- **Real-world analogies:** express courier vs. standard freight; spot checks
  vs. full audit.
- **Translate to money, time, risk.** Zero acronyms.
- **Pushing back on a senior stakeholder:** anchor on *their* goals; show a
  concrete comparison (cost, time-to-value, maintenance); persuade without
  condescension.
- **"Is this AI worth it?" (60s):** lead with business metrics — time saved,
  errors reduced, adoption — and be honest about limits.
- **Architecture reviews:** agenda up front, decisions as options with
  trade-offs, listen before defending, leave with owners + action items.

## Ownership Stories (7.1–7.3)

- **7.1 Bias for action:** shipped 80% in two weeks → name the deliberate
  trade-offs, transparent limits, iterate on feedback. Opposite of
  perfectionist paralysis.
- **7.2 Solution rejection:** users didn't adopt → curiosity about the
  friction, modify or *discard* code. Never blame users.
- **7.3 Extreme accountability:** "I owned this pipeline, my validation failed
  here, here's the fix." No finger-pointing at upstream teams.
