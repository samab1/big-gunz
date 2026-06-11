# APP.md — app architecture & decisions (living document)

Update this file (including the dated changelog at the bottom) with every code change.

## What it is

A single-file workout app: `index.html`, vanilla HTML/CSS/JS, zero dependencies,
no build step. Dark theme, mobile-first (user uses it on their phone mid-workout).

**Live:** https://samab1.github.io/big-gunz/ — GitHub Pages, "deploy from branch",
branch `main`, folder `/ (root)`. Deploys ~1 min after every push to `main`.
The repo was made public to enable Pages on a free plan. Push directly to `main`
(user-approved; no PRs needed).

## Why these choices

- **Single file, no framework:** user demanded "extremely simple, nothing fancy";
  one file means trivial hosting, no toolchain for future agents to break.
- **Embedded YouTube (youtube-nocookie.com iframes):** user is a visual learner and
  explicitly wants videos playing **inside** the app, never redirecting to YouTube.
- **Lazy iframes, one at a time:** iframe is created when a card opens and destroyed
  when it closes — keeps the page light and stops background audio.
- **Stick-figure inline SVG icons:** user doesn't know exercise names; icons are
  recognition aids. Consistent style: 64×64 viewBox, stroke-only, accent color.
- **localStorage, no backend:** no accounts, no sync, no tracking overhead — fits the
  "no counting anything" requirement. Single user, single device assumption.
- **Reorder via arrow buttons, not drag-and-drop:** reliable on mobile, less code.
- **Checks are manual with an "Uncheck all"** (no auto-reset by date) — simplest
  mental model; user resets at the start of a session.

## Data model (in `index.html`)

- `EXERCISES = { A: [...], B: [...] }`, each item:
  `name, meta (sets×reps·weight), cue (one-liner), why (explanation), grow (form/growth tips), video (YouTube ID), icon (inline SVG string)`.
- `DAY_NOTES = { A, B }` — HTML strings explaining each day.
- localStorage keys:
  - `bigGunzDay` — last selected day ("A"/"B").
  - `bigGunzDoneA` / `bigGunzDoneB` — JSON array of **exercise names** checked off.
  - `bigGunzOrderA` / `bigGunzOrderB` — JSON array of names defining custom order.
  - ⚠️ Done/order state is keyed by exercise **name** — renaming an exercise silently
    resets its state (acceptable; degrade is graceful via the `indexOf === -1` path).

## UI structure

Header → Day A/B tabs → day note → progress row ("n of N done", Reorder, Uncheck all,
Reset order while reordering) → exercise cards → coach's rules footer.

Card collapsed: icon | name/meta/cue | check circle. Tap head = expand; tap circle =
toggle done (stopPropagation; separate targets). Expanded: video, "Open on YouTube"
fallback link, "WHY IT'S HERE" block, "FOR GROWTH" block. `body.reordering` class
swaps check circles for ▲▼ buttons and disables card expansion.

## Videos

Selection criteria: short, clear, beginner-friendly, from channels known to allow
embedding (Buff Dudes, ScottHermanFitness, Onnit, NASM, StrongFirst). Chosen via web
search; **embeddability could not be verified from the dev sandbox** (YouTube blocked
there) — if the user reports "Video unavailable" on an exercise, swap that video.

| Exercise | Video ID | Channel |
|---|---|---|
| Goblet squat | MxsFDhcyFyE | Buff Dudes |
| Incline DB press | hChjZQhX1Ls | ScottHermanFitness |
| KB clean & press | km3f8_rpDdg | Onnit |
| Incline DB fly | bDaIL_zKbGs | ScottHermanFitness |
| KB halo | XzqwVP_wSpc | (exercise demo) |
| Dead hang | Nc-JGSZZMAQ | (exercise demo) |
| KB deadlift | MJPGkNqAXzg | NASM |
| One-arm DB row | tLnlWj7LQ34 | Buff Dudes |
| KB swing | yHxcTn1UeAc | StrongFirst |
| Alternating DB curl | sAq_ocpRh_I | ScottHermanFitness |
| DB shrug | xDt6qbKgLkY | ScottHermanFitness |

## Dev workflow

1. Edit `index.html`.
2. Syntax-check the inline JS:
   extract `<script>` body to a file and run `node --check` on it.
3. Commit with a clear message, push to `main`.
4. Update this file + `COACH.md` if content changed. Tell the user to refresh in ~1 min.

There are no tests and no CI — the syntax check and care are the safety net.

## Changelog (append-only, newest last)

- **2026-06-11** — v1: Day A/B tabs, exercise cards with SVG icons, inline
  youtube-nocookie embeds (lazy, one at a time), coach rules footer.
- **2026-06-11** — Added per-exercise "why it's here" / "for growth" blocks inside
  expanded cards; done-checkboxes with per-day persistence, progress count,
  "Uncheck all"; expanded day notes and A/B explanation in coach footer.
- **2026-06-11** — Reorder mode: ▲▼ arrows per card, per-day saved order,
  "Reset order" button. Card expansion disabled while reordering.
