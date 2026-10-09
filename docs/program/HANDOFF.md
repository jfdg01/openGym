# Handoff: no-weak-links strength program

Picked up from a Claude chat session on 2026-10-09. Read this file first, then issue #1 (the map) and issue #2 (open decisions). The issues are the source of truth. This file is a snapshot.

## What this is
Javier (60.6 kg, 170 cm; kung fu Mon–Thu 21:30–22:30, which he never misses) wants a long-term gym program in which every movement on a list of ~100 gets measurably stronger, with no weak links. He logs in openGym (this fork). The program logic will be built here: issues #3–#11.

## How we got here
1. A first 6-day program and a Google Sheet tracker (`legacy-strength-tracker.xlsx`) were drafted quickly and reviewed by 5 agents. Javier then judged it "vibecoded": too many unchecked assumptions.
2. A grilling session (mattpocock `grilling` skill) restarted from intent. The settled decisions are below and in #1.
3. A deep-research pass checked the field's methods (`research-report.md`, with notes in `research-notes/`). Key findings:
   - Progression algorithms barely differ in results. Measurement noise differs ~4× between movements (≈4% barbell e1RM, ≈15–20% DIY isometrics).
   - Each movement needs only 1–2 hard sets per exposure. Strength doesn't transfer between movements, though, so the real constraint is coverage, which is a scheduling problem.
   - Weak links must be judged from noise-scaled trends over 8–12 exposures (Hopkins), never from single comparisons or Poliquin-style ratios. Left:right on the same exercise is the one ratio worth keeping.
4. Javier compared his own `jfdg01/gym-app` (a hobby FastAPI PWA) with openGym. openGym won because it already has a queue, L/R sets, RIR/RPE, timed sets, e1RM and an offline mode.

## Settled decisions
- **Goal:** no weak links in general strength. No power or conditioning work for now: the bet is that a complete body transfers to kung fu.
- **Priority:** kung fu always wins over the gym.
- **Horizon:** one year, to summer 2027, then re-design around the post-master's schedule.
- **Coverage:** full. Every movement is trained and gets a number.
- **Skill items:** scapular anterior tilt, toe abduction, foot arch, tibial rotation and chin tuck are logged, but kept out of the strength ranking.
- **Schedule:** 2–5 sessions a week, irregular. When he trains, he does the whole session, so there is no short version.
- **Sessions:** full-body, in a plain rotation (openGym's queue) now. "Most overdue first" comes later (#11).
- **Progression:** one rule, double progression counted per session. Compounds use low rep ranges, small items higher ones.
- **Effort:** RIR logged on every set. Targets are RIR 1–3 on compounds and 0–2 on small items, with a to-failure calibration set about every 4 weeks.
- **Deloads:** openGym's per-exercise reset (×0.9 after 3 stalls), not calendar-based.
- **Baseline:** no special baseline event. Each movement's start value is the median of exposures 3–5, then a rolling 8–12-exposure trend. Weak-link judgement switches on after ~8 exposures.
- **Weak-link signals:** growth against own start value, in noise units, plus L:R. Reference ratios are hints only.
- **Data sources:** mainly training logs. Crane-scale force tests only where logs don't compare fairly (Javier will buy a crane scale).
- **Bodyweight and nutrition:** out of scope.
- **Readiness questionnaire:** dropped. The only fixed constraint is Mon–Thu class nights.
- **Rollout:** rules run as an analysis on exports for 8–12 weeks (#10). Only the ones that hold up get coded into the app.
- **Issues** use gym-app's labels: triage roles plus `wayfinder:*` (see gym-app `docs/agents/`).

## Still open (resume grilling here, tracked in #2)
From the last round, unanswered:
- **Q1:** minutes per full session. This sets sets per session; about 25 fit in 70 minutes.
- **Q2:** what time he trains on Mon–Thu. Before ~18:30 needs no class-day rule. Evening training needs one, e.g. RIR ≥ 3 on lower-body compounds.
- **Q3:** a global deload on top of the per-exercise reset. Recommended: not now; let #10 report whether stalls cluster.
- **Q4:** fork only, or upstream pull requests for #4, #5 and #7. Recommended: fork first, upstream once proven.
- **Q5:** heavy (3–5) and moderate (6–8) variants for compounds. Recommended: not now.
- **Q6:** language for the analysis script. Recommended: JS under `scripts/`, so it can move into `src/lib`.

Home sessions (photos sent 2026-10-09). The home kit is an adjustable dumbbell handle with spin-locks, ProIron plates (≥ 2 × 1.25 kg plus others), ≥ 2 × 10 kg Amonax plates, an 8 kg kettlebell, a loading pin with carabiner, a chain with carabiners, a pinch block, an adjustable dip station, a red band, a two-pad bench (probably hyperextension) and an ab bench. A dip belt is possible but unconfirmed. On top of that come the earlier items: ankle strap, neck harness, gripper and finger/thumb bands.
- **H1:** exact inventory (handles, plate counts, bench type, dip belt).
- **H2:** role of home sessions. Recommended (c): a home version of each gym session, plus the small items done at home.
- **H3:** home exercises share history with gym versions only when implement and set-up match. Movement tags (#3) group them for coverage.
- **H4:** a doorway pull-up bar for vertical pull at home. Recommended yes.
- **H5:** home lower body is single-leg work, Nordic and back extension. Heavy bilateral squat and deadlift stay at the gym.

After these: tiers (which movements get main-lift dose, which get maintenance, which may slide on short weeks) and the target trend per tier. Then write the actual rotation (gym and home sessions) as openGym routines.

## Useful facts
- **Gym gear (no purchases needed):** ankle strap, neck harness, gripper and finger/thumb extensor bands. To buy: fractional plates (~€20) and a crane scale (~€15).
- **Migrating from gym-app:** `tools/to_opengym.py` in gym-app exports its Strength history and current weights as an openGym backup. Run it on the server, which deploy.sh reaches as the `oracle` ssh host, then use Import backup.
- **openGym today:**
  - e1RM is Epley on reps only (no RIR), capped at 12 reps, taking the session's best set (`frontend/src/lib/onerm.js`).
  - Double progression has no RIR gate. Increments use a fixed `inc` grid. There is no gap or layoff handling (`frontend/src/lib/progression.js`).
  - An optional read-only MCP server (`mcp/`) can expose workouts to an LLM client, which is useful for running #10 from Claude.
- **Upstream roadmap overlaps:**
  - v1.4.0 (2026-11-15) changes exercise ids. This affects #3.
  - v1.4.2 brings the AMRAP flag (#154), multi-formula 1RM (#155) and triple progression.
  - v1.4.3 brings RPE/RIR targets (#153) and 5/3/1 waves.
- **Contributing:** CONTRIBUTING.md requires training logic in `src/lib` with a test beside it, no new dependencies, and every UI string in all locales.

## Suggested first command in the CLI
Run the `grilling` skill on issue #2, starting with Q1–Q6 and H1–H5 above. Record each answer in #1 under "Decisions so far".
