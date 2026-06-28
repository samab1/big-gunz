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
  `name, meta (sets×reps·weight), cue (one-liner), why (explanation), grow (form/growth tips), primary ([muscle keys]), secondary ([muscle keys]), feel (form-check sentence), video (YouTube ID), icon (inline SVG string)`.
- **Muscle map:** `bodyMap(primary, secondary)` returns inline SVG of two figures
  (front + back). Each figure is a smooth shared silhouette (`SILPATH`, viewBox
  140×300) in neutral, with muscle-group shapes drawn on top — primary = accent bright,
  secondary = dim, unworked = neutral grey. `muscleChips()` renders plain-language name
  chips. Muscle keys are the keys of `MNAME` (chest, shoulders, biceps, triceps,
  forearms, abs, traps, lats, upperback, lowerback, glutes, hamstrings, quads, calves).
  Hand-built SVG **on purpose** — no library (would violate the single dependency-free
  file rule). To add a muscle, add a shape in both relevant figures + an `MNAME` entry.
  The `feel` field is the "which muscle should I feel" form-check the user asked for.
  NOTE: "shoulders" lights both front and rear delts (one key) — a deliberate
  simplification, so pressing also tints the back delts. Fine for a beginner app.
- **Verifying SVG visually:** there's no browser preview in chat, but a Chromium binary
  is preinstalled at `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`. Render any
  HTML to PNG and Read it back to iterate on visuals:
  `<chrome> --headless --no-sandbox --disable-gpu --force-device-scale-factor=2 --screenshot=out.png --window-size=300,800 file://ABS/PATH.html`
  (a stray dbus ERROR line is harmless). This is how the muscle figures were tuned.
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
| Chest-supported DB row | jnj4Lc4Ir3U | (exercise demo) |
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
- **2026-06-28** — Swapped Day B "One-Arm Dumbbell Row" → "Chest-Supported DB Row"
  (user back pain; see COACH.md). New name resets that card's done/order state — fine,
  graceful. New video jnj4Lc4Ir3U, new bench-row icon.
- **2026-06-28** — Added an "updated YYYY-MM-DD" stamp in the footer. Purpose: user runs
  the app as an iOS home-screen web clip, which caches aggressively; the stamp lets them
  confirm a refresh actually pulled the latest. **Bump this date on any user-visible
  change** (it's near the end of `index.html`, after the coach `.coach` div).
- **2026-06-28** — Added per-exercise muscle map: inline-SVG front+back body figures
  with worked muscles highlighted (`bodyMap()`), plain-language muscle chips, and a
  "Feel it here" form-check line. New exercise fields: `primary`, `secondary`, `feel`.
  Lives in a TARGETS block at the top of each expanded card. No external library
  (deliberate — keeps the single-file rule).
- **2026-06-28** — Redesigned the muscle figures (user: first version "does not look
  good"). Replaced disconnected blocky ellipses/rects with a smooth shared silhouette
  + muscle overlays; better proportions, reads as a real body. Tuned by rendering with
  the preinstalled Chromium (see "Verifying SVG visually" above).
