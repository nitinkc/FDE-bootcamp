# Phase 5 — FDE Excellence

**Goal:** Operate as a trusted customer-facing engineer.
- [ ] Completed a mock FDE-style discovery session.

### Discovery & Scoping

1. **"An operations director says: 'Our team spends too much time on task handoffs and things fall through the cracks. Build me an AI tool.' Run your first two discovery sessions."** *(5.1)*
   - Strong answer: asks "why" before architecture, shadows operators, maps the real manual process, separates process vs. data vs. tooling problems, lands a 2–3 week MVP.
2. **"Discovery reveals they don't need AI at all — just a filtered daily priority list with clear ownership. What do you do?"** *(5.1 probe)*
   - Strong answer: ships the simple thing, says so plainly, frames it as the win it is.
3. **"Translate 'make our reporting smarter' into a scoped deliverable. Walk through requirement → architecture."**
   - Strong answer: identifies the decisions users actually make, defines a measurable success metric, phases the scope, calls out assumptions explicitly.
4. **"How do you design validation and workflows for operators under time pressure — catch errors early without creating alert fatigue?"** *(4.2)*
   - Strong answer: tiered validation, selective friction on irreversible actions, draft/undo, human-readable errors.

### Communication & Leadership

1. **"Explain the trade-off between latency, compute cost, and accuracy to a business leader with no CS background."** *(5.2)*
   - Strong answer: real-world analogies, translates to money/time/risk, zero acronyms.
2. **"A senior stakeholder insists on the complex, 'sexier' solution you know is wrong. How do you push back?"** *(1.3 probe, adapted)*
   - Strong answer: anchors on their goals and risks, offers a concrete comparison (cost, time-to-value, maintenance), persuades without condescension.
3. **"Run an architecture review with a skeptical customer platform team. How do you structure it and handle pushback?"**
   - Strong answer: clear agenda, decisions presented as options with trade-offs, listens before defending, leaves with action items and owners.
4. **"An exec asks, 'Is this AI project actually worth it?' Give your 60-second answer."**
   - Strong answer: leads with business metrics (time saved, errors reduced, adoption), honest about risks and limits, no hype.

### Ownership Stories (verify your STAR bank covers these)

1. **"Tell me about a tool you built that users didn't adopt. What did you change?"** *(7.2)*
   - Strong answer: humility + curiosity about friction; modifies or discards code; doesn't blame users.
2. **"Tell me about a time something you owned went wrong. How did you communicate and fix it?"** *(7.3)*
    - Strong answer: "I owned this, here's where my validation failed, here's the fix" — no finger-pointing.

### 4.2 — Designing for Human Error in High-Consequence Workflows

- **Question:** "Operators are inputting data under significant daily time pressure. How do you design backend validation and frontend application workflows to catch mistakes early without causing workflow fatigue or system sluggishness?"
- **Good signs:** tiered validation — instant client-side format checks paired with authoritative server-side business rules; selective friction — confirmation modals and required reason codes for irreversible actions, non-blocking warnings for low-risk anomalies; draft state saving, undo, clear human-readable errors.
- **Red flags:** hard validation stops for every minor warning, creating alert fatigue that drives operators back to manual offline spreadsheets.

### 5.1 — Tackling Vague Business Requests

- **Question:** "Imagine an operations director tells you: 'Our team spends way too much time managing daily task handoffs, and things are falling through the cracks. Can you build an AI/automation tool to fix it?' How would you run your first two discovery sessions to figure out what to actually build?"
- **Good signs:** asks "why" repeatedly before proposing architecture; shadows operators to map the real manual process, informal handoffs, and tracking spreadsheets; separates whether the breakdown is a process problem, data visibility problem, or tooling problem; identifies a focused MVP deliverable in 2–3 weeks.
- **Red flags:** immediately diagrams an elaborate multi-agent AI system without validating how tasks actually get done on the ground.
- **Follow-up probe:** "What if discovery reveals the operators don't need AI at all — just a simple daily filtered priority list with clear ownership?"

### 5.2 — Communicating Technical Trade-Offs to Non-Engineers

- **Question:** "How would you explain the trade-offs between speed (latency), operational compute cost, and accuracy/reliability to a business leader who has zero computer science background?"
- **Good signs:** intuitive real-world analogies (express courier vs. standard freight; spot checks vs. full forensic audits); translates technical trade-offs into financial cost, turnaround time, and operational risk.
- **Red flags:** dense academic/engineering jargon; impatience or condescension toward non-technical stakeholders.

### 7.1 — Bias for Action vs. Perfectionism

- **Question:** "Academic and research programs reward being exhaustive and 100% theoretically sound. In an enterprise forward-deployed role, you often need to ship a 75–80% complete solution within two weeks to gather real user feedback. Tell me about a time you stepped away from perfectionism to ship fast. What compromises did you make, and how did it turn out?"
- **What to evaluate:** intentional technical-debt trade-offs, transparent communication of limitations, comfort in iterative feedback loops.
- **Red flags:** paralysis when requirements are incomplete; refuses to deploy until every edge case is proven.

### 7.2 — User Empathy & Handling Solution Rejection

- **Question:** "Describe a scenario where you spent significant effort building a technical tool, script, or pipeline, but the intended users pushed back or simply did not use it. How did you handle that feedback, and what did you change?"
- **What to evaluate:** humility, emotional resilience, curiosity about operational friction, willingness to modify or discard code to solve the user's real problem.
- **Red flags:** blames end users ("they weren't tech-savvy enough"); resentment toward operational feedback.

### 7.3 — Extreme Accountability

- **Question:** "Tell me about a time a project or pipeline you owned went wrong — a bug caused a disruption, a deadline was missed, or an underlying assumption was proven false. How did you communicate the issue to teammates and fix it?"
- **What to evaluate:** immediate personal ownership ("I owned this pipeline, here is where my validation failed, and here is how I fixed it") vs. finger-pointing ("the upstream team broke the schema without telling me").


