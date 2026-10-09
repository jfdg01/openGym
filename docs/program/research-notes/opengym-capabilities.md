# openGym capabilities and upstream roadmap

Research for jfdg01/openGym#16 (child of the map #12). Question: what openGym supports now, and
what the upstream roadmap adds, for logging a no-weak-links program (see `CONTEXT.md`:
movement, exercise, exposure, weak link, skill item).

Sources: this repo at `f049465c` (identical to `upstream/main` on 2026-10-09), `ROADMAP.md`, and
upstream issues on DuarteSantos8/openGym read on 2026-10-09. Paths are relative to
`frontend/src/` unless they start with `api/`, `mcp/` or a top-level file.

## Summary

| Capability | Now | Upstream plan |
|---|---|---|
| e1RM formula | Epley in the app; Brzycki and Lombardi exist but only MCP exposes a choice | Seven-formula weighted estimate with RIR, PR #195 / issue #155 (v1.4.2; ROADMAP lists a picker for v1.3.11) |
| e1RM set selection | Best single completed work set per session, reps 1..12, warm-ups and assisted lifts out, per-side sides scored on their own | Rep cap 15 for the weighted estimate (#195) |
| RIR / RPE logging | Per set (and per side), one scale per profile, 0.5 steps; read by Stats only | Target RIR/RPE in the plan, v1.4.3 (#153); effort ranges (#154) |
| Progression rules | off, linear, Greyskull LP, double, add-time; per routine line | Triple progression and v2 engine v1.4.2 (#179, #186); %1RM and training max, wave/5-3-1, auto-regulation v1.4.3 (#153, #70, #120) |
| Deload / reset | Reactive per exercise after N stalls, factor 0.9 (0.5..0.95), Epley-targeted for linear/double | Programmes with planned deload and rest weeks, v1.4.1 (#159) |
| AMRAP | Only Greyskull's final set | Universal AMRAP flag first, v1.4.2 (#154) |
| L/R sets | Rep sets: `sides: {L, R}` with own weight, reps, effort, done. Timed holds: L and R rows | none needed |
| Timed / isometric | `mode: 'time'` sets `{sec, w}`; add-time policy; chart = longest hold | Time per side (#444, v1.3.11) |
| Routine queue / rotation | `S.queue` ordered queue + in-app rotation that refills (v1.3.10) | Programmes over weeks (#159), phases (#57), v1.4.1 |
| Exports / backups | Full-state JSON, JSON+media zip, Android auto-backup (newest 14), plan bundle, copy-as-text; server `db.json.bak`; read-only MCP | Admin per-user export v1.4.5; state file stays the export format after DB storage (Later) |
| Exercise ids | Built-ins `"0001"`..; custom `"c"+uid`; imports `im…` | **v1.4.0 (2026-11-15): new catalogue, built-in ids change**, migrated on first start |
| Muscle tags | 18 canonical muscle slugs, primary/secondary weights | Movement direction and compound/isolation, #379 (no milestone) |
| Movement (joint action) tag | Missing | Missing |
| Custom exercises | Yes, synced in `S.customEx`, muscle chips, own media | Parity with built-ins #199; delete bug #378 |
| CSV export | Missing (CSV import only) | Not planned |

## Details

### e1RM: formula and set selection (supported)

- Formulas: `FORMULAS = {epley, brzycki, lombardi}`, `DEFAULT_FORMULA = 'epley'`
  (`lib/onerm.js:19-27`). `REP_CAP = 12`: above it no estimate (`lib/onerm.js:17`, `:37`). One
  rep returns the weight unchanged (`lib/onerm.js:39`). Rounded to 0.1.
- Set selection: `bestSetOf` takes the single best completed reps-mode set of an entry, skipping
  warm-up rows via `metricRowsForEntry`; drop-set drops are not scored (`lib/onerm.js:47-63`). A
  per-side set is scored on each side's own weight and reps (`lib/onerm.js:54-56`).
  Assisted machines are excluded entirely (`lib/onerm.js:51`).
- Trend: one point per workout, the best set that day (`e1rmSeries`, `lib/onerm.js:76-84`);
  all-time best keeps its source set (`best1RM`, `lib/onerm.js:88-92`).
- No formula setting in the app: the 1RM sheet says "Epley formula" (`sheets.jsx:855`). The MCP
  tool `estimate_1rm` accepts `formula: epley|brzycki|lombardi` (`mcp/src/tools.js:401-412`).
- RIR is not read by the estimate. Timed and cardio sets never produce one.
- Separate Epley helper for deloads halves the total reps of per-side work
  (`lib/progression.js:66-77`).
- Upstream: #155 (milestone v1.4.2) asks for a reliability-weighted multi-formula estimate with
  Epley kept as the default shown. PR #195 implements seven formulas (adds O'Connor, Mayhew,
  Wathan, Lander), RIR-aware effective reps, a `weighted` formula capped at 15 reps and an
  accuracy index. ROADMAP v1.3.11 lists "a 1RM formula picker (#195)", but the PR has no
  milestone and the owner said he reviews it with the new progression engine (#312).

### RIR / RPE logging (supported, retrospective only)

- A set carries `rir` or `rpe`, never both; the profile setting `S.effort` is `none|rir|rpe`
  (`lib/history.js:82-83`, `:107-110`). RIR 0..10, RPE 6..10, step 0.5. Switching scale never
  rewrites old sets.
- Per-side sets rate each side (`lib/workout-model.js:190-196`).
- Stats aggregates in RIR (`rirOf = rir ?? 10 - rpe`, `lib/effort.js:22-23`); "hard set" is RIR
  <= 3 (`HARD_RIR`, `lib/effort.js:16`).
- Progression never reads effort (no `rir`/`rpe` in `lib/progression.js`).
- Imports keep it: Hevy RPE (`lib/import-hevy.js:263-264`), CSV RIR column
  (`lib/import-csv.js:87`, `:571`).
- Missing: a target RIR/RPE on the plan. Upstream #153 (v1.4.3): load as absolute, %1RM or auto,
  plus target RPE/RIR; owner: "a real gap", PR #168 is the first piece.

### Progression rules and deload / reset (supported, reactive)

- Policies: `off, linear, greyskull, double, time` (`lib/progression.js:25-47`). Reps mode
  allows the first four, timed mode `off|time`, cardio `off` (`:28-32`). Default for reps mode is
  linear (`policyFor`, `:102-110`). Pyramid sets are never progressed (`:104`).
- Increments: `cfg.inc`, else 5 kg for legs/back/hips/glutes and 2.5 kg otherwise (10/5 lb)
  (`lib/progression.js:84-94`); timed default +5 s (`:95`, `:392`).
- Only the planned sets decide the next step; extra sets do not (`readSession`,
  `lib/progression.js:262-311`). Each routine progresses its own line of a lift (#216,
  `sessionsFor`, `:320`).
- Bodyweight work climbs reps, then adds sets up to `MAX_BW_SETS = 6` (`:98`, `:458-484`).
- Deload: after `DELOAD_AFTER = {linear: 3, greyskull: 1, double: 3, time: 3}` stalls
  (`:52`); factor `cfg.deloadFactor`, default 0.9, range 0.5..0.95 (`:51-62`). Linear and double
  pick an Epley-matched weight/reps candidate on the load grid (`selectDeloadCandidate`,
  `:158-208`, used at `:518-540`); timed backs off and rebuilds (`:448-449`). A weight change, a
  plan edit, or (double) beating the run's best ends a stall streak (`stallCount`, `:351-376`).
- Missing: planned deload weeks, mesocycles, %1RM loads, RIR-driven autoregulation.
- Upstream: v1.4.1 programmes with deload and rest weeks (#159); v1.4.2 triple progression
  (#179) inside a generic v2 prescription engine (#186); v1.4.3 %1RM/training max and target
  RPE/RIR (#153), wave/5-3-1 (#70), warm-up generator (#156), periodisation and RPE
  auto-regulation (#120).

### AMRAP (Greyskull only)

- `readSession` treats the last set as the AMRAP set (`lib/progression.js:305`); doubling the
  target gives a double jump, Greyskull only (`:578`).
- Upstream #154 (v1.4.2): universal AMRAP flag plus set/rep/load/effort ranges; owner: "AMRAP
  flag first (smallest, most asked)".

### L/R (unilateral) sets (supported)

- Flag `cfg.side` (`isPerSide`, `lib/history.js:52`). Rep targets step by 2
  (`lib/history.js:58`).
- A per-side rep set stores `sides: {L, R}`, each with weight, reps, effort, done and its own
  drop/rest-pause; the row keeps summaries (r = L+R, w = max, done = both)
  (`lib/workout-model.js:155-171`, `:190-200`). Volume reads each side (`:185-189`).
- A per-side timed hold becomes one L row and one R row per planned set (`lib/history.js:525`
  onward; doubling read back in `lib/progression.js:270-276`).

### Timed and isometric sets (supported as holds)

- Mode `time` (`modeOf`, `lib/history.js:31-36`); sets `{sec, w}`, so a weighted hold logs its
  load. Isometrics are timed holds; there is no separate isometric type.
- Progression: `time` policy adds `cfg.inc` seconds (default 5) once every set reaches the goal
  (`lib/progression.js:288-296`, `:442-450`).
- History chart for timed work plots the longest hold in seconds, ignoring load
  (`lib/exercise-history.js:10-15`). No e1RM or strength metric for holds.
- Upstream: time per side (#444, v1.3.11).

### Routine queue / rotation (supported, v1.3.10)

- `S.queue = {ids, since, startsOn, label, strict?, rotationId?}`: ordered sessions; the first not
  done is today's, whatever the weekday (`lib/queue.js:1-25`). Any API client may PUT a queue (a
  "planner").
- `S.rotation = {id, sequence, label}` is the in-app definition; a pass it owns refills when
  complete (`lib/rotation.js:1-31`, `refillAfter` `:200`). The weekday model (`S.week`,
  `S.dayPlan`) stays as the alternative.
- Upstream: programmes grouping routines over weeks (#159) and session phases with
  completion-only exercises kept out of volume and PRs (#57), both v1.4.1.

### Exports and backups

- Export backup: the whole state `S` as pretty JSON, `opengym-backup-YYYY-MM-DD.json`
  (`views/Settings.jsx:256-266`); with media as a zip (`views/Settings.jsx:278-284`). Import
  accepts both (`views/Settings.jsx:764`).
- Android auto-backup of the state JSON, newest 14 kept, optional chosen folder
  (`lib/mobile.js:270`, `:280`).
- Server: `db.json` plus `state-<uid>.json` under `DATA_DIR`, atomic writes, a `db.json.bak`
  copy (`api/server.js:122-152`); `GET /api/data` returns the user's state
  (`api/server.js:2098`).
- Plan bundle export/import (`lib/plan-share.js:178`, `:208`); copy a workout as text
  (`lib/workout-text.js:17`).
- MCP (read-only): `list_routines, get_routine, get_week_plan, list_workouts, get_workout,
  get_bodyweight, estimate_1rm, muscle_balance, preview_session` (`mcp/src/tools.js:101-532`).
- Imports: Strong, Hevy, FitNotes CSV and Apple Health (`docs/DATA_IMPORTS.md:10-27`).
- Missing: a CSV or flat per-set export. Analysis outside the app reads the state JSON.
- Upstream: admin per-user export (v1.4.5); DB storage (Later, #191) keeps the state file as the
  import/export and backup format.

### Exercise ids (change coming in v1.4.0)

- Built-ins: four-digit string ids from the generated dataset (`"0001"`,
  `lib/exercises-data.js`), indexed in `EXIDX` (`lib/exercises.js:46-47`).
- Custom: `'c' + uid()` (`sheets.jsx:1096`); importer-created: `importId('im', …)`
  (`lib/import-hevy.js:181`).
- Upstream ROADMAP v1.4.0 (due 2026-11-15): the catalogue is replaced by a licensed one,
  "exercise ids change"; history, routines, custom exercises, favourites and import aliases are
  migrated on first start. No upstream issue specifies the mapping; milestone v1.4.0 holds only
  #145 (progress graph per set number) and #188 (icons) open.
- Inference: anything outside the app that stores built-in ids (notes, spreadsheets, scripts)
  breaks at v1.4.0; custom-exercise ids are user data and should survive the migration.

### Muscle tags (supported, muscle level only)

- Built-ins carry `bp` (body part), `tg` (target), `mg`, `sm` (secondary) and an owner overlay of
  `primaries`/`secondaries` (`lib/exercises.js:6-25`).
- Canonical vocabulary: 18 slugs (`trapezius, deltoids, chest, upper-back, serratus, biceps,
  triceps, forearm, abs, obliques, lower-back, gluteal, quadriceps, hamstring, adductors,
  hip-flexors, calves, tibialis`) (`lib/muscles.js:17-23`); primary weight 1, secondary lower
  (`muscleWeightsOf`, `lib/muscles.js:191-224`).
- No movement or joint-action tag (for example hip internal rotation). No rotator cuff, hip
  rotator, neck or foot slug.
- Upstream #379 (no milestone): derive push/pull/static direction and compound/isolation. Still
  not a joint action.

### Custom exercises (supported)

- Stored in synced `S.customEx` (`lib/exercises.js:59-96`); created with
  `{id, n, bp, desc, tg, sm, muscleGroups, primaries, secondaries, eq, custom: true}`
  (`sheets.jsx:1097`). Routine config adds mode, `side`, `bodyweight`, `assisted`, `inc`.
  Pictures since v1.3.9.
- Open upstream: cannot delete a custom exercise (#378); built-in/custom parity (#199).

## What this means for the program

- One movement maps to one custom exercise. The name carries the movement, because no field
  holds it. Muscle tags cannot tell movements apart.
- e1RM works for loaded rep work up to 12 reps, but only with Epley in the app. Holds have no
  strength number beyond the longest duration.
- RIR can be logged per set (and per side) and read from the state JSON. Nothing in the app acts
  on it before v1.4.3.
- Any external tooling keyed on built-in exercise ids has to be re-keyed after v1.4.0.
