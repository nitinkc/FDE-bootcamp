# FDE Prep Journal

A MkDocs site for tracking Google Cloud Forward Deployed Engineer (FDE) interview
and career preparation — daily/weekly learning log, skill matrix, project work,
and interview prep, all versioned in Git.

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

1. Copy `docs/journal/2026/week-01.md` to `week-02.md` (etc.), clear the fields, fill in
   the week's priorities.
2. Add the new week to the `nav:` list in `mkdocs.yml`.
3. Fill in each day's session as you go — this is your daily discipline log.
4. Sunday: update `docs/progress/readiness-dashboard.md` with new readiness % and
   review the accountability checkpoint.
5. Every 2 weeks: revisit `docs/progress/skill-matrix.md` and update strength ratings.
6. As concepts solidify, promote notes from the weekly journal into the relevant
   `docs/topics/*` page as a permanent, organized reference (the journal is a stream;
   the topic notes are the distilled result).
7. Commit and push. One commit per session is a good habit — it's also a visible
   proof-of-consistency trail if it ever comes up in an interview.

## Structure

```
docs/
  index.md                      Home / current status snapshot
  progress/
    readiness-dashboard.md      Readiness % over time, risks, milestones
    skill-matrix.md             Full skill matrix, updated biweekly
  journal/2026/
    week-01.md ...              One page per week — the daily log
  phases/
    phase-1-foundation.md ...   Static long-term roadmap, checked off over time
  projects/healthcare-rag-platform/
    overview.md                 Business problem, scope, GCP/AI components
    architecture.md             Current architecture, kept up to date
    decisions.md                Design decision log (interview gold)
    changelog.md                What changed, when
  topics/
    gcp/ vertex-ai/ rag/ agentic-systems/ system-design/
                                 Evergreen distilled notes per subject
  interview-prep/
    mock-interviews.md          Log of mock interview reps + feedback
    behavioral-stories.md       STAR-format story bank
    system-design-drills.md     Practice reps log
  resources/
    resources.md                Curated links only — mandatory/important topics
```
