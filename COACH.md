# COACH.md — workout context (living document)

Update this file whenever the program changes or the user reports anything
(progress, soreness, boredom, likes/dislikes). Journal entries are append-only.

## The user

- Beginner: a few weeks of training when the program started (June 2026).
- ~183 cm, ~87 kg (reported 2026-07-08). Trains in the morning.
- **Big goal: get bigger (hypertrophy).** Upper-body biased interest, but the program
  deliberately stays balanced (legs/pull included) because that serves the goal.
- Visual learner; does not know exercise names — needs videos and icons.
- Wants simple, low-injury-risk training. No complex movements.
- Likes kettlebells. Likes keeping the same gear.
- Trusts Huberman (→ Andy Galpin) and Rogan (→ Pavel Tsatsouline / StrongFirst style)
  as sources; recommendations land better when framed through those.
- Trains at home, 3 days/week (e.g. Mon/Wed/Fri), alternating Day A / Day B.

## Equipment

- Dumbbells, with heavier ones available (can progress in weight).
- Kettlebells: 16 kg and 20 kg.
- Adjustable bench (incline works).
- Pull-up bar (used for dead hangs so far).

## Current program (since 2026-06-11, v2 since 2026-07-08)

Progression rule (double progression): finish all sets with good form and ~2 reps left
in the tank → add weight next session; if no heavier weight exists (KB moves), add reps
up to the top of the range first, then weight. **The last set of every exercise must
feel genuinely hard** ("could I do 5 more?" → too easy). Slow 2–3 s lowering everywhere.
Rest ~90 s big moves, ~60 s isolation. Warm-up: 2–3 min arm circles, bodyweight squats,
light halos, short hang.

### Day A — Push & Squat
| Exercise | Sets × Reps | Weight | Why it's in |
|---|---|---|---|
| Goblet squat (KB) | 3×10–15 | 16→20 kg | Legs drive whole-body growth; back-friendly squat |
| Incline DB press | 3×8–10 | progressive | Main chest/size builder; upper chest focus |
| KB clean & press | 3×6/side | 16 kg (20 last set) | Shoulders/traps + full-body; Pavel style |
| Incline DB fly | 2×10–12 | light | Loaded stretch = strong growth signal; finisher |
| DB lateral raise | 3×12–15 | light | Side delts = width; nothing else hits them directly (added v2) |
| KB halo | 2×8/dir | 16 kg | Shoulder health/mobility insurance |
| Dead hang | 2×max | bodyweight | Grip, spine decompression, pull-up step 1 |

### Day B — Pull & Hinge
| Exercise | Sets × Reps | Weight | Why it's in |
|---|---|---|---|
| KB deadlift | 3×10–15 | 20 kg | Hinge pattern, glutes/hams; back-safety school |
| Chest-supported DB row | 3×10 | progressive | Back/V-shape builder; bench supports torso so lower back can't strain |
| KB swing | 3×12 | 16 kg | Hip power + conditioning; Pavel/Rogan staple |
| Alternating DB curl | 3×12/arm | progressive | Direct biceps (user favorite, kept from old plan) |
| Lying DB triceps extension | 3×10–12 | light | Triceps = 2/3 of arm size; had zero direct work (added v2) |
| DB shrug | 3×12 | heavy | Traps; visible mass, kept from old plan |
| Dead hang | 2×max | bodyweight | Same as Day A |

Order is flexible within a rule: big lifts first while fresh, isolation later, dead
hang last. The app lets the user reorder.

## History of the user's training (pre-program)

Original self-made routine (all pushing/arms, no pulling or hinge): DB alt curls 12×3,
incline DB fly 6×2, DB shrug 6×3, KB clean & press 6×3, KB halo 12×3, goblet squat
12×3, dead hangs in between. Identified gaps: no back work, no hamstrings/glutes,
getting repetitive. The current program kept everything they liked and filled the gaps.

## Likes / dislikes

- Likes: kettlebells, A/B simplicity, short clear videos, checking things off.
- Dislikes: repetitive routines, complex/risky movements, counting/tracking overhead.

## Future coaching ideas (not yet active)

- Pull-up progression once dead hang reaches an easy 60+ seconds.
- A 24 kg kettlebell when 20 kg goblet squats/deadlifts get easy.
- Swap-in variation menu if boredom returns (e.g. floor press, hammer curls,
  KB front rack hold) — keep the same patterns, change the flavor.
- Periodic check-in questions: how's recovery, any joint complaints, which exercise
  feels best/worst.

## Journal (append-only, newest last)

- **2026-06-11** — Program v1 created from user's original routine. Added: incline DB
  press, KB deadlift, one-arm DB row, KB swing. Structure: A/B split, 3 days/week.
  User confirmed: 3 days/week, has bench + pull-up bar + heavier dumbbells.
- **2026-06-11** — User asked whether exercise order is strict. Coached: big lifts
  first, isolation later, hang last; otherwise flexible. Reorder feature added to app.
- **2026-06-28** — User reported the **one-arm DB row hurts their back**. Root cause:
  the bent-over hinge holds the torso up and loads the lower back. Replaced it with
  **chest-supported DB row** on the incline bench (torso fully supported → no lower-back
  load), same horizontal-pull / lat / mid-back stimulus, simpler form. Program stays
  balanced (still has the pulling pattern Day B needs). Watch: confirm the new movement
  is pain-free; if any back pull persists, look at the KB deadlift/swing hinge form next.
- **2026-06-28** — Added a visual muscle map to each exercise (user doesn't know muscle
  names, is a visual learner). Each exercise now also carries a "Feel it here" cue — the
  muscle the user should feel working, as a self-check that their form is right. If a
  future program change adds/edits an exercise, set its `primary`/`secondary` muscles and
  `feel` cue too (see APP.md for the muscle keys).
- **2026-07-08** — User check-in (~4 weeks into program v1): asked for a full program
  review. Feedback: workouts don't feel hard enough ("could be going stronger") and he's
  "not finishing as satisfied" regarding muscle growth. Goal restated: get bigger; still
  wants simple, low-injury-risk exercises. Coach review findings: (1) most likely culprit
  is effort — beginner probably stopping sets too far from failure; coached that the last
  set of each exercise should feel genuinely hard (~2 reps left, not 5); (2) progression
  is about to hit the kettlebell ceiling (goblet squat/deadlift capped at 20 kg) —
  recommended double progression (grow reps 10→15 before adding weight) and eventually a
  24 kg bell; (3) two real gaps for the "bigger" goal: **no side-delt work** (recommend DB
  lateral raise, Day A) and **no direct triceps work** (recommend lying DB triceps
  extension, Day B) — both simple, low-risk, dumbbell-only; (4) reminded that at 4 weeks
  visible size is mostly still ahead, and food (protein) + sleep gate growth.
  **No program change applied yet — awaiting user's go-ahead on the two new exercises.**
- **2026-07-08** — User shared stats and diet: ~183 cm, ~87 kg, trains in the morning.
  Typical day: chicken salad lunch + light dinner ("relatively normal and healthy").
  Asked how much protein to put in a post-workout drink. Coached: **40 g whey in the
  shake** (simple: two scoops), but flagged the real issue — his daily total is likely
  ~80–100 g vs the ~150–170 g/day (~1.6–2 g/kg) that the "get bigger" goal needs, and a
  "light dinner" works against a size goal. Advice: shake after morning workout, protein
  at every meal (palm-of-meat rule), make dinner the anchor meal, don't fear eating more
  on training days. Watch: ask at a future check-in whether the shake/protein habit stuck.
- **2026-07-08** — **Program v2.** User approved the review's recommendations; asked
  where to add the new exercises, whether anything should be removed, and to update
  reps/weights. Applied: (1) added **DB lateral raise 3×12–15 light** to Day A after the
  incline fly (isolation slot, before halo/hang); (2) added **lying DB triceps extension
  3×10–12 light** to Day B after the curls (arms finish, before shrug/hang); (3) nothing
  removed — both days are still ~7 exercises / ~45 min, all other work is pulling its
  weight, so removal would cost more than it saves; (4) reps updated for the KB ceiling:
  goblet squat and KB deadlift are now **3×10–15 double progression** (reps first, then
  weight), and the coach rules in the app now state the double-progression rule and the
  "last set must feel genuinely hard / could-I-do-5-more test". Videos: lateral raise
  3VcKaXpzqRo, triceps extension MO_03opCc0g (both ScottHermanFitness — embeddability
  unverified from sandbox as usual; swap if "Video unavailable"). Watch next check-in:
  are sessions feeling hard again, elbow comfort on the triceps extension, and whether
  he bought the 24 kg bell.
