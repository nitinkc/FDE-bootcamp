# FDE Prep Journal

[https://nitinkc.github.io/forward-deployed-engineer-gcp/](https://nitinkc.github.io/forward-deployed-engineer-gcp/)

A MkDocs site for tracking Forward Deployed Engineer (FDE) interview and career
preparation — learning roadmap, skill matrix, project work, and interview prep,
all versioned in Git.

## Setup

```bash
pip install -r requirements.txt
mkdocs serve   # preview locally at http://127.0.0.1:8000
```

## Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

## Weekly Workflow

1. Work the current phase's checklist; capture evidence in its "Notes / Evidence"
   section.
2. Update strength ratings in `docs/phases/skill-matrix.md` as skills move.
3. Update the Current Status table in `docs/index.md` as readiness changes.
4. Run reps from `docs/interview-prep/` and the phase deep dives —
   self-interview questions, drills from the Prep Plan, STAR stories.
5. Commit and push. One commit per session is a good habit — it's also a visible
   proof-of-consistency trail if it ever comes up in an interview.

## Structure

```
docs/
  index.md                      Home / current status snapshot
  phases/
    phase-1-foundation.md ...   Static long-term roadmap, checked off over time
    skill-matrix.md             Full skill matrix, updated periodically
  projects/healthcare-rag-platform/
    overview.md                 Business problem, scope, GCP/AI components
    architecture.md             Current architecture, kept up to date
  interview-prep/
    prep-plan.md                Gap-driven prep plan and drills
    behavioral-stories.md       STAR-format story bank
```
