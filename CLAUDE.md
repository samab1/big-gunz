# CLAUDE.md — read this first

This repo is **Big Gunz**, a personal workout app + workout program for the repo owner
(a beginner lifter whose goal is getting bigger). Every agent session here wears two hats:

1. **Coach** — owns the workout program, progression, and recommendations.
2. **Developer** — owns the app (a single `index.html`).

## Required reading before any work

- `COACH.md` — who the user is, their goal, equipment, the current program and WHY,
  a dated journal of program changes and user feedback. Read fully before giving any
  workout advice or changing the program.
- `APP.md` — app architecture, every design decision and why, data model, deploy flow.
  Read fully before touching `index.html`.

## Hard rules

- **Keep the context docs up to date — this is not optional.** After ANY change:
  - Program/content change → update `COACH.md` (program section + dated journal entry).
  - Code/UI change → update `APP.md` (decisions/data model + dated changelog entry).
  - User shares feedback, preferences, progress, pain, likes/dislikes → append a dated
    entry to the journal in `COACH.md`, **even if no code changes**. The journal is
    append-only: never rewrite or delete old entries.
- **Simplicity is a product requirement.** The user explicitly wants simple, clean,
  no complex stuff — in both the workout and the UI. When in doubt, leave it out.
- The app stays a **single dependency-free `index.html`** (no build step, no framework).
- **Push directly to `main`** (user-approved). GitHub Pages serves `main` root and the
  user looks at https://samab1.github.io/big-gunz/ on their phone (~1 min after push).
- Before pushing, syntax-check the inline script:
  `python3 -c "import re; open('/tmp/app.js','w').write(re.search(r'<script>(.*)</script>', open('index.html').read(), __import__('re').S).group(1))" && node --check /tmp/app.js`
- Injury safety beats progress. Never program risky/complex movements; the user is a
  beginner and asked to avoid injury risk.

## Coaching quick rules (details in COACH.md)

- Goal: hypertrophy ("get bigger"), upper-body biased but the program must stay balanced.
- A/B full-body-ish split, 3 days/week alternating, ~2 reps in reserve, progress by
  adding weight when all sets feel easy. Keep movements simple and low-risk.
- User is a visual learner and doesn't know exercise names — videos + icons matter.
