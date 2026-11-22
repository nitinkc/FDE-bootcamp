# Lesson 04 — LLM Foundations

*Phase 1 · AI Foundations questions.*

## Tokens, Context Window, Temperature (explain simply)

- **Token** — the unit the model reads/writes; ~¾ of a word. Practical
  consequence: **you pay per token**, and long docs get truncated.
- **Context window** — the model's working memory: everything it can "see" at
  once (prompt + history + output). Overflow it and content gets dropped or the
  call fails.
- **Temperature** — a randomness dial. 0 ≈ deterministic and safe for
  extraction/formatting; higher = more varied/creative, more error-prone.

## Fixing Inconsistent, Badly Formatted Output — lever order

Cheap/easy first, heavyweight last:

1. **System instructions** — state the exact format and rules explicitly.
2. **Few-shot examples** — show 2–5 input→output pairs in the desired shape.
3. **Structured output** — JSON schema / response schema enforcement.
4. **Temperature** — lower it for consistency.
5. **Only then** — switch model or consider tuning. Fine-tuning is the *last*
   resort, not the first.

## Pro vs Flash (model tiers)

- **Flash-tier:** fast, cheap, good enough for simple tasks — classification,
  extraction, short answers, high volume.
- **Pro-tier:** slower, pricier, better reasoning — complex multi-step tasks,
  hard edge cases.
- **Route by difficulty:** send easy queries down-tier, hard ones up-tier.
  **Measure quality per route — don't guess.**

## Vertex AI vs Gemini API directly

- **Gemini API (AI Studio):** fastest path to a prototype; minimal setup.
- **Vertex AI:** when you need enterprise plumbing — VPC/private networking,
  IAM governance, eval tooling, Model Garden, tuning, data-residency and
  compliance controls.
- Rule of thumb: prototype on the API, productionize on Vertex when governance
  requirements appear.
