# Algorithms and computational models used by training apps and research to plan and auto-adjust resistance training

Scope note: these notes cover how apps and research models decide what to train and how much. They separate published or documented logic from marketing claims, cover research through 2026, and end with ideas usable by a single user (n-of-1) who logs weight, reps and RIR per set and trains 1–6 days a week. In this survey's research budget, the help-center pages of RTS/TrainHeroic, JEFIT, Boostcamp and Strong were not fetched. They appear under Gaps rather than being described from memory.

## 1. Commercial and open apps: inputs, rules, outputs, and what is published

### Takeaway
No commercial app publishes its actual math. RP, MacroFactor/SBS, Fitbod, Juggernaut AI, Alpha Progression and Hevy Trainer document only their inputs and qualitative rules ("more sets if pump is low", "lower load if the set was harder than intended"). The only fully transparent progression logic is in scriptable or open tools (Liftosaur's Liftoscript, openGym's code) and in the published SBS spreadsheet rules (training-max adjustment per rep over or under target). The documented app behaviours reduce to a few rule families:
- double progression, with or without an expanded rep range
- load-from-RPE/RIR tables plus e1RM (Epley)
- AMRAP- or RIR-driven training-max adjustment
- per-muscle weekly set progression driven by feedback (soreness, pump, workload)
- per-muscle recovery percentage used to pick exercises

### Cited Findings

**RP Hypertrophy (Renaissance Periodization)**
- Inputs: post-session ratings of pump, muscle soreness and perceived workload, which feed future prescriptions — [RP help center](https://help.rpstrength.com/hc/en-us/articles/32600173777815-How-does-the-app-determine-when-to-add-weight-reps-and-sets)
- Load rule: "weight is increased by a few percentage points each week". If the next available weight step is too large (e.g. 10 lb to 15 lb dumbbells), reps are added instead — [RP help center](https://help.rpstrength.com/hc/en-us/articles/32600173777815-How-does-the-app-determine-when-to-add-weight-reps-and-sets)
- Set rule, qualitative only:
  - weak pump, minimal soreness and an easy workload, so "the app will usually assign you more sets"
  - strong pump, soreness that recovers on time and near-limit workload, so no change
  - intense pump, soreness that is not recovered in time and an overwhelming workload, so fewer sets
  - The user can add or delete sets manually.
  - No numeric thresholds are published. — [RP help center](https://help.rpstrength.com/hc/en-us/articles/32600173777815-How-does-the-app-determine-when-to-add-weight-reps-and-sets)
- The underlying RP methodology, as described by a third party:
  - volume landmarks MEV, MAV and MRV, counted in weekly hard sets per muscle
  - start the mesocycle at MEV and add about 1 set per muscle per week if recovery is on track
  - hold volume if soreness, pump or performance stalls
  - deload if the user fails to beat last week's reps on 2 or more exercises
  - don't add sets to a muscle that is still sore
  - RIR progresses from about 3 to 0–1 across a 4–6 week mesocycle
  - deload at about 50% volume and about 10% lower intensity
  - The source is a commercial third-party page that cites no primary studies for these rules. — [Arvo, "RP Training"](https://arvo.guru/resources/methods/rp-training)

**MacroFactor Workouts (Stronger By Science team; package id com.sbs.train)**
- Inputs: logged weight and reps, the RIR target, logged performance compared with expectations, and the accumulated history for each exercise — [MacroFactor help 373](https://help.macrofactorapp.com/en/articles/373-why-does-the-app-sometimes-recommend-lowering-weight-or-reps)
- Rule: a set that is harder than intended (e.g. 6 of 8 reps, or 1 RIR when 2 was targeted) means future load "may be adjusted downward". Recommendations are described as "never punitive". No magnitudes are published. — [MacroFactor help 373](https://help.macrofactorapp.com/en/articles/373-why-does-the-app-sometimes-recommend-lowering-weight-or-reps)
- "Smart Progression":
  - prefers weight changes within the programmed rep range
  - the "Expand Rep Range" option, e.g. after 100 lb x 8, suggests 100 x 9 rather than 105 x 8 when the jump is too big
  - "Weight Match" keeps the previous set's weight when that still gives a good target
  - a warning appears when no available weight keeps the next set inside the range (e.g. 8–10 reps at 2 RIR after logging 15 reps)
  - It gives no immediate recommendation without history.
  - No e1RM formula is disclosed. — [MacroFactor help 305](https://help.macrofactorapp.com/en/articles/305-understanding-and-using-smart-progressions)
- Missed sessions: "If you miss workouts or take time off, your program does not change." Programs use training cycles, not a calendar. After a gap, new sets update the recommendations, and they "may be adjusted" if performance changed. No detraining thresholds are published. — [MacroFactor help 382](https://help.macrofactorapp.com/en/articles/382-what-happens-to-my-program-if-i-miss-workouts-or-take-time-off)

**SBS programs (Greg Nuckols spreadsheets; secondary summary)**
- RTF (reps to failure) variant: the last set is taken to failure.
  - Each rep beyond the target raises the training max (TM) by about 0.5%.
  - Missing by 2 or more reps lowers the TM by about 1% per missed rep.
  - Hitting the target exactly means no change.
  - — [Lift Vault summary](https://liftvault.com/programs/strength/stronger-by-science-sbs-program-bundle-by-greg-nuckols/)
- RIR variant: do sets until the RIR target is reached, then count the sets.
  - More than about 6 sets: TM +2% (default).
  - Fewer than about 4 sets: TM −5% (default).
  - This is a secondary summary, so the exact values should be checked against the official spreadsheet. — [Lift Vault summary](https://liftvault.com/programs/strength/stronger-by-science-sbs-program-bundle-by-greg-nuckols/)

**Fitbod**
- Recovery model:
  - Each muscle group gets a recovery percentage from 0 to 100%, based on recent training.
  - "Full recovery typically takes up to 7 days."
  - Fresher muscles are prioritized, and fatigued ones get lighter or alternative work.
  - The user can override the value, and Apple Health, Health Connect and Strava activity is also included.
  - — [Fitbod help: How Fitbod Creates Your Workout](https://help.fitbod.me/hc/en-us/articles/360004429814-How-Fitbod-Creates-Your-Workout)
- The blog says muscles trained heavily in the past 48–72 h score lower, citing Schoenfeld (2010). No decay curve, half-life or per-muscle rate is published. — [Fitbod blog, algorithm](https://fitbod.me/blog/fitbod-algorithm)
- Exercise selection: all 800+ exercises are scored on recovery, trainer-rated fit, the user's add/remove/favourite history, the split, and available equipment. The weights of the scoring function are not published. — [Fitbod blog](https://fitbod.me/blog/fitbod-algorithm)
- Load:
  - 1RM is estimated with "established prediction equations (such as the Epley formula)".
  - "Max Effort Days" periodically re-test capacity.
  - The "mStrength" model alternates heavier/low-rep and lighter/high-rep sessions.
  - RIR logging is said to sharpen estimates, but no formula is given.
  - Starting loads come from aggregate data for similar users and are deliberately conservative.
  - — [Fitbod help](https://help.fitbod.me/hc/en-us/articles/360004429814-How-Fitbod-Creates-Your-Workout); [Fitbod blog](https://fitbod.me/blog/fitbod-algorithm)
- Marketing claims without specifics: "400M+ logged workouts" and "machine learning on your behavior". No model type, features or validation are disclosed. — [Fitbod blog](https://fitbod.me/blog/fitbod-algorithm)

**Juggernaut AI (JTS)**
- Inputs:
  - an onboarding questionnaire (sex, age, height, weight, experience, strength, sticking points, lifestyle)
  - pre-session readiness (sleep, mood, energy, soreness)
  - RPE on the top set and the back-down set
  - end-of-week, end-of-block and post-meet feedback
  - — [JTS help: How JuggernautAI is individualized](https://help.jtsstrength.com/en/articles/3-how-juggernautai-is-individualized-to-you)
- Rules as described:
  - MEV and MRV are adjusted "based on factors such as gender, height, and body weight"
  - readiness modifies "volume or weight as needed"
  - the readiness score is "a running, weighted average", with weights not disclosed
  - next sets are tweaked within the session
  - adjustments are made weekly and per block
  - No formulas, thresholds or deload criteria are published. — [JTS help](https://help.jtsstrength.com/en/articles/3-how-juggernautai-is-individualized-to-you)
- Marketing: "over 10 quadrillion potential program variations", with no stated method — [JTS help](https://help.jtsstrength.com/en/articles/3-how-juggernautai-is-individualized-to-you)

**Alpha Progression**
- Per-set recommendations of weight, reps and optionally RIR:
  - based on previous workouts and on sets already done in the current workout
  - uses the gym's real available loads
  - adds reps before a large jump (e.g. 7.5 to 10 kg is +33%)
  - avoids a big barbell reload for a negligible gain
  - recommendations can go down, and the estimated 1RM or 10RM can decrease
  - plans are not tied to calendar dates and continue in sequence
  - No formulas are published. — [Alpha Progression guide](https://alphaprogression.com/en/blog/alpha-progression-guide)

**Hevy**
- The core logger pre-fills previous workout values — [Hevy help](https://help.hevyapp.com/hc/en-us/articles/36011896355479-How-to-Use-Previous-Workout-Values-to-Improve-Performance-in-Hevy)
- Hevy Trainer (Pro):
  - 11 onboarding questions
  - programs "generated using an algorithm and do not rely on AI"
  - it tells the user when and how much to increase weight "based on performance"
  - No rules, increments, RPE use or missed-session logic are documented. — [Hevy Trainer explained](https://help.hevyapp.com/hc/en-us/articles/38385724273047-Hevy-Trainer-Explained-How-It-Builds-Your-Workout-Program)

**Liftosaur (fully documented, scriptable)**
- A program is plain text: `Exercise / sets x reps / weight | % | @RPE / timers / progress: ...`, with `# Week` and `## Day` sections. `@8` derives the weight from built-in RPE tables, and `+` marks AMRAP, a logged RPE, or an asked weight. — [Liftoscript docs](https://www.liftosaur.com/doc/liftoscript)
- Built-in progressions:
  - `lp(increase, attempts, currentAttempt, decrease, decreaseAttempts, currentDecreaseAttempt)` is linear progression with a success streak and a failure-driven decrease
  - `dp(increase, minReps, maxReps)` is double progression
  - `sum(repThreshold, weightIncrease)` adds weight when total reps across sets exceed a threshold
  - — [Liftoscript docs](https://www.liftosaur.com/doc/liftoscript)
- Custom progress scripts:
  - They run after the workout.
  - They read `weights, reps, completedReps, completedRPE, RPE, rm1, bodyweight, numberOfSets` and write `weights, reps, RPE, timers, numberOfSets, rm1`.
  - Persistent `state.*` variables hold counters such as attempts.
  - Built-ins include `rpeMultiplier(reps, rpe)` (the 1RM fraction for a rep/RPE pair), `calculate1RM(weight, reps)` (Epley), `calculateTrainingMax`, and `roundWeight`/`increment`/`decrement` for the available plates.
  - `update:` scripts run during the workout after each set, so the next sets can be autoregulated (e.g. a back-off set from the top-set result).
  - Exercises can change one another's state via tags.
  - — [Liftoscript docs](https://www.liftosaur.com/doc/liftoscript)

**openGym (DuarteSantos8)**
- The repository and releases are public (e.g. v1.2.2) — [GitHub releases](https://github.com/DuarteSantos8/openGym/releases); [Gitea mirror](https://gitea.com/DuarteSantos/openGym)
- The logic summarised in the task context (off/linear/greyskull/double/time policies, Epley e1RM, deload to 0.9 after 3 stalls, strength-balance ratios, rotating queue) was not re-verified against source code here.

### Inferences
- Across MacroFactor, RP and Alpha Progression the shared core is load-step-aware double progression. If the next plate jump overshoots the target, add a rep. If a set comes in harder than the target RIR, step down. Increments come from the available equipment rather than a fixed percentage. This is fully implementable with logged weight, reps and RIR.
- RP's set autoregulation is a per-muscle weekly volume controller: start at MEV, add about 1 set per week, and hold or deload on bad feedback. It is useful for hypertrophy accessories, and it needs one or two short post-session questions per muscle (soreness on return, workload).
- SBS RTF/RIR is the most transparent published autoregulation of a training max, with a percent change per rep surplus or deficit. It maps directly onto the per-set reps and RIR data the user already logs.
- "AI" and "ML" in Fitbod, Juggernaut AI and Hevy are marketing-level claims without published models. For an n-of-1 system they offer nothing reproducible beyond their documented rule shapes.

### Gaps
- No primary source was fetched for RTS/TrainHeroic RPE-based load selection, JEFIT, Boostcamp or Strong. Strong is generally a pure logger, but that is not verified here.
- RP's exact feedback scales, its joint-pain question and its numeric thresholds are not published in the fetched help article. The RIR sequence of 3, 2, 1, 0 and then deload is commonly reported but was not confirmed in a primary source here.
- The MacroFactor/SBS e1RM model and the size of its adjustments are undisclosed.
- The official SBS spreadsheet values were not verified (only the Lift Vault secondary summary).

## 2. Research models: fitness-fatigue (Banister), PerPot, recovery time courses, ML and Bayesian prediction, individualized dose-response

### Takeaway
Banister-type impulse-response models fit resistance-training data only moderately (rats: R² about 0.53). They are ill-conditioned (the two gains k1 and k2 correlate at r = 0.88–0.99), and simulations say they need measurement error of about 4% CV or less and frequent testing to predict usefully. PerPot fit slightly better in a 4-subject strength pilot. The best-validated individual prediction tools for strength are much simpler: individual RIR-velocity and load-velocity regressions and RPE/RIR scales. ML work so far is small-sample and is about estimating RPE, not prescribing programs.

### Cited Findings

**Banister and fitness-fatigue models in resistance training**
- Rats on progressive ladder climbing, 4 weeks, n = 11:
  - The two-component Banister model fit best: R² 0.53, adjusted R² 0.47, with τ1 = 5.31 d, τ2 = 4.3 d and recovery after one bout of about 1.07 d.
  - The variable dose-response extension (Busso) gave no significant improvement, probably because the overload was too low.
  - The authors stress small samples and moderate R².
  - — [Philippe et al. 2015, BioMed Res Int](https://pmc.ncbi.nlm.nih.gov/articles/PMC4324815)
- The same paper cites Busso et al. (1990) as a systems model in elite weightlifters linked to hormones. That is the key human resistance-training reference, but its results were not retrieved here. — [Philippe et al. 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4324815)
- Simulation of the fitness-fatigue model applied to resistance training (2.1 million simulations):
  - Measurement CVs above about 4% "will not provide satisfactory results".
  - Each 1% of CV adds about 21–25 W of median prediction error.
  - Each day of lower testing frequency adds about 19–26 W.
  - k1 and k2 correlate at r = 0.88–0.99, a sign of ill-conditioning and overfitting.
  - Weekly 1RM tests reported in resistance-training studies have CVs of 1–3%.
  - — [Stephens Hemingway et al. 2020, IJSSC](https://rgu-repository.worktribe.com/OutputFile/691845)
- Review of extensions:
  - Hill saturation of inputs
  - Busso's variable dose-response (in-sample R² 0.931–0.958 vs 0.917–0.943, with no out-of-sample test)
  - Kalman-filter state-space models (Kolossa et al. 2017)
  - non-linear power-term models
  - Most studies lacked out-of-sample validation. Open R code is available at fitnessfatigue.com and github.com/bsh2/fitness-fatigue-models.
  - — [Swinton, Stephens Hemingway et al. 2021, SportRxiv Part II](https://rgu-repository.worktribe.com/OutputFile/1871154)
- PerPot vs the fitness-fatigue model in strength training, 4 subjects, 8 weeks of unilateral curls and leg extensions, with load as force impulse and performance as peak power:
  - PerPot fit better: ICC 0.73 vs 0.67, mean relative deviation 3.68% vs 4.29%.
  - PerPot predicted the final 1 week better: 3.93% vs 5.97%.
  - — [ECSS 2009 abstract](https://lida.sport-iat.de/twm/Record/4019682?lng=en)
- Recent model work (titles only, not read in depth):
  - a 3-D impulse-response model by energy system — [arXiv 2503.14841](https://arxiv.org/pdf/2503.14841)
  - a control-theory perspective on the fitness-fatigue model — [arXiv 2609.26506](https://arxiv.org/pdf/2609.26506)

**Recovery time course (the basis for per-muscle recovery curves)**
- Ten trained men did bench press and full squat under three protocols: 3x5 (of a possible 10), 6x5 (of 10), and 3x10 to failure.
  - Training to failure caused larger drops in velocity and countermovement jump (CMJ).
  - Recovery was significantly faster between 24 and 48 h for the non-failure protocols.
  - "training to failure slows down recovery up to 24–48 h post-exercise"
  - — [Morán-Navarro et al. 2017, Eur J Appl Physiol (PubMed 28965198)](https://pubmed.ncbi.nlm.nih.gov/28965198/)

**Validated individual load and effort estimation**
- Individual RIR-velocity relationships in the back squat (n = 46, 2,607 observations):
  - Individual models had about twice the R² of pooled models.
  - Session-1 individual models predicted RIR in session 2 within 2 reps at all loads. Pooled models managed this only at 80–90% 1RM.
  - Error fell at higher loads.
  - — [Jukic et al. 2024, Physiol Rep](https://pmc.ncbi.nlm.nih.gov/articles/PMC10901726)
- Load-velocity 1RM prediction, an individual-participant meta-analysis (20 studies, about 434 participants):
  - The standard error of the estimate was about 9.8% of 1RM.
  - It systematically overestimated 1RM by 4.5 kg (3.7%).
  - It is best used to track trends.
  - — [Greig et al. 2023, Sports Med](https://rgu-repository.worktribe.com/OutputFile/1947441)
- RIR-based RPE scale: RPE correlated inversely with velocity, r = −0.88 in experienced squatters and r = −0.77 in novices. The study proposes the scale for regulating daily load. — [Zourdos et al. 2016, JSCR](https://openrepository.aut.ac.nz/items/efef3b25-6701-4fb5-bb82-55fcd2a26027/full)

**Machine learning**
- RPE estimated from inertial and EMG sensors on dumbbell curls (69 sets):
  - A random forest was best, with 41.4% exact and 85.9% within ±1 RPE.
  - Eccentric time was the top feature.
  - Generalizability is a stated challenge.
  - — [Thomas & Wahlström 2025, arXiv 2510.03197](https://arxiv.org/abs/2510.03197v1)

**Individualized dose-response ("training to the individual")**
- Trained individuals whose weekly volume was set at 20% above their own previous volume grew more than with a fixed volume. This is the Scarpelli et al. 2020 study as summarized by SBS. — [PubMed 32108724](https://pubmed.ncbi.nlm.nih.gov/32108724/); [SBS research spotlight](https://www.strongerbyscience.com/research-spotlight-muscle-growth/)
- A follow-up compared increasing vs maintaining volume relative to each person's previous volume in trained males (title only; results not retrieved) — [PubMed 39665246](https://pubmed.ncbi.nlm.nih.gov/39665246/)

### Inferences
- With logged weight, reps and RIR, every set already gives an e1RM-like performance observation. Daily e1RM noise from RIR misjudgement (about ±1 rep, i.e. about ±3%) sits near the edge of the ≤4% CV the fitness-fatigue simulation calls for. A Banister fit per lift is therefore feasible only with dense data on the same lift and with strong priors or fixed time constants. A model with fixed τ (about 5 d fitness, about 2–4 d fatigue, roughly in line with the rat data) and gains fitted by regularized least squares, or a Kalman filter, is the realistic version. Free-parameter fits will overfit.
- The 24–48 h recovery penalty of training to failure, plus Fitbod's "up to 7 days" heuristic, support a simple per-muscle exponential recovery curve with a 1–3 day time constant that grows with RIR-0 sets. This is a heuristic, not a validated model.
- Individual RIR or e1RM profiles beat population tables. An app should calibrate each user's rpeMultiplier-style table from their own logs rather than use generic RPE charts.

### Gaps
- Results of Busso et al. (1990) on weightlifters, and any human resistance-training validation of Banister with out-of-sample prediction, were not retrieved.
- No published Bayesian, hierarchical prediction model for gym-goer strength progression was found in this search.
- No validated per-muscle fatigue/recovery model with published parameters was found. Fitbod's is proprietary.
- Full results of the Scarpelli 2020 and 2024 studies (CSA numbers, sample) could not be retrieved because PubMed showed a CAPTCHA.

## 3. Handling irregular schedules: missed sessions, rotating queues, most-overdue scheduling

### Takeaway
The dominant documented pattern is "sequence, not calendar". MacroFactor and Alpha Progression simply continue to the next workout after a gap and let new performance data correct the loads. Fitbod is the only documented app that schedules by state: it picks muscles by recovery percentage, a de facto "least fatigued / most ready first" rule. No app documents a published "most overdue movement" scheduler or explicit detraining math.

### Cited Findings
- MacroFactor:
  - Programs "use training cycles" rather than calendar weeks, and the program "does not change" when sessions are missed.
  - The user can skip a workout or pause logging.
  - Recommendations may adapt after time off according to performance, with no thresholds published.
  - — [MacroFactor help 382](https://help.macrofactorapp.com/en/articles/382-what-happens-to-my-program-if-i-miss-workouts-or-take-time-off)
- Alpha Progression: plans are not tied to calendar dates, and the user continues in sequence — [Alpha Progression guide](https://alphaprogression.com/en/blog/alpha-progression-guide)
- Fitbod: exercise selection is constrained by per-muscle recovery from 0 to 100%. Fresher muscles are prioritized, and outside activity is imported. — [Fitbod help](https://help.fitbod.me/hc/en-us/articles/360004429814-How-Fitbod-Creates-Your-Workout)
- Liftosaur: a program is a list of weeks and days that the user advances through. Progress scripts run after each completed instance of an exercise, not by date. — [Liftoscript docs](https://www.liftosaur.com/doc/liftoscript)

### Inferences
- For 1–6 irregular days a week, a "most overdue" queue works naturally. Each movement pattern or lift has a target frequency (e.g. squat every 3–4 days). Its due-score is the time since it was last trained divided by its target interval, gated by a per-muscle recovery estimate from section 2. On each session, take the highest-scoring items that fit the time budget. This generalizes openGym's rotating queue and Fitbod's recovery-gating. It is an inference and not documented in any app.
- Progressing per exercise instance (as in Liftosaur and MacroFactor) rather than per calendar week makes progression robust to irregular frequency. Weekly-volume controllers (RP-style) instead need a rolling 7-day window.
- For long gaps, a reasonable approach is to let the first post-gap sets re-anchor the e1RM, as MacroFactor and Alpha Progression do implicitly. An optional conservative start (e.g. −5–10% after 2 or more weeks) has no documented app formula.

### Gaps
- No primary documentation was found for detraining discounts in any app.
- No published algorithm for scheduling by movement due-time was found.

## 4. Exercise to muscle to movement-pattern taxonomies and open datasets

### Takeaway
Open datasets tag primary and secondary muscles, equipment, force (push/pull/static) and mechanic (compound/isolation), but none of those found tags movement patterns such as hinge, squat, horizontal push or vertical pull. Those tags would have to be added by hand on top of free-exercise-db or wger.

### Cited Findings
- free-exercise-db (yuhonas):
  - 800+ exercises under the Unlicense (public domain), one JSON file each
  - fields `force`, `level`, `mechanic`, `equipment`, `primaryMuscles[]`, `secondaryMuscles[]`, `category`, `instructions`, `images`
  - `force`, `mechanic` and `equipment` are nullable or incomplete
  - no movement-pattern field
  - — [GitHub yuhonas/free-exercise-db](https://github.com/yuhonas/free-exercise-db)
- wger: a public REST API (base https://wger.de) offering exercises, muscles and equipment. The third-party listing rates its documentation as poor; the official docs are at wger.de/en/software/api. — [public-api.org listing](https://public-api.org/api/1208/wger)
- ExRx licenses its exercise data commercially (not open) — [ExRx licensing](https://exrx.net/store/other/licensing)
- Other datasets: the exercemus exercises repository and sergei-argutin/exercise-dataset on GitHub, and the MuscleWiki API (commercial). These were found in search but not examined. — [exercemus/exercises](https://github.com/exercemus/exercises); [exercise-dataset](https://github.com/sergei-argutin/exercise-dataset); [MuscleWiki API docs](https://api.musclewiki.com/documentation.md)
- Fitbod uses a proprietary 800+ exercise library scored per muscle group — [Fitbod blog](https://fitbod.me/blog/fitbod-algorithm)

### Inferences
- A practical schema is: exercise, then primary and secondary muscles with weights (e.g. 1.0 and 0.5 sets credited), then one movement pattern, then equipment and increment. This supports per-muscle weekly-set counting (RP-style), recovery gating (Fitbod-style) and pattern-based due scheduling (section 3).

### Gaps
- openGym's 1,324-exercise library schema was not inspected in this research.
- Whether any open dataset ships movement-pattern tags was not determined (exercemus and MuscleWiki were not examined).

## 5. Ideas worth implementing for a single user with honest data (n-of-1)

### Takeaway
Implement transparent, documented rules first:
- an equipment-aware double progression with RIR, in the style of MacroFactor and Alpha Progression
- SBS-style training-max adjustment from the rep or RIR surplus on the last set
- an individually calibrated RPE/RIR table, which is better than generic charts (Jukic 2024)
- an optional RP-style weekly set controller for accessories
- a due-score scheduler gated by recovery

A Banister fitness-fatigue model is a "nice to have" analytics view, best run with fixed time constants. It does not reliably drive decisions given RIR noise.

### Cited Findings
- Per-set e1RM from reps plus RIR uses Epley or `rpeMultiplier(reps, rpe)` tables. Liftosaur exposes both as primitives. — [Liftoscript docs](https://www.liftosaur.com/doc/liftoscript)
- Training-max adjustment of about +0.5% per extra rep and about −1% per missed rep when 2 or more reps short (RTF), or +2%/−5% by RIR set counts — [Lift Vault SBS summary](https://liftvault.com/programs/strength/stronger-by-science-sbs-program-bundle-by-greg-nuckols/)
- Add reps when the plate jump is too large, and step down when a set is harder than its RIR target — [MacroFactor help 305](https://help.macrofactorapp.com/en/articles/305-understanding-and-using-smart-progressions); [MacroFactor help 373](https://help.macrofactorapp.com/en/articles/373-why-does-the-app-sometimes-recommend-lowering-weight-or-reps); [Alpha Progression guide](https://alphaprogression.com/en/blog/alpha-progression-guide)
- Individual RIR-velocity and effort profiles predict better than pooled ones — [Jukic et al. 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10901726)
- Fitness-fatigue predictions need a measurement CV of about 4% or less and frequent testing. k1 and k2 are collinear. — [Stephens Hemingway et al. 2020](https://rgu-repository.worktribe.com/OutputFile/691845)
- Failure training delays recovery by 24–48 h — [Morán-Navarro et al. 2017](https://pubmed.ncbi.nlm.nih.gov/28965198/)
- Personalizing volume to the user's own previous volume (+20%) beat standardized volume in trained subjects — [SBS spotlight on Scarpelli 2020](https://www.strongerbyscience.com/research-spotlight-muscle-growth/)

### Inferences
1. **e1RM per set.** Compute e1RM = w × (1 + (reps + RIR)/30), i.e. Epley with reps-to-failure, or a personal table. Smooth it with an EWMA or Kalman filter per exercise. Stall detection works better on the smoothed trend than on "missed reps 3 times".
2. **Load selection.** Target weight = smoothed e1RM × f(target reps, target RIR), rounded to the available increments. If the rounding error exceeds about 2.5%, keep the weight and adjust reps instead (double-progression fallback).
3. **Autoregulated training max.** After each exercise instance, nudge the training max by the RIR or rep surplus (SBS-style percentages). Deload when the smoothed e1RM declines over N exposures, rather than after a fixed number of stalls.
4. **Volume.** Credit weekly sets per muscle as primary 1.0 and secondary 0.5, over a rolling 7 days. Optionally use an RP-style rule: +1 set per week if soreness was resolved by the next exposure and the workload was easy, hold otherwise, and back off on two degraded signals.
5. **Scheduling.** Due-score = days since last exposure divided by the target interval, multiplied by a recovery factor. The recovery factor is 1 − e^(−t/τ), with τ larger after RIR-0 sets. Fill the session from the highest scores.
6. **Analytics.** A Banister model with fixed τ (fitness about 5 d, fatigue about 2–4 d, as heuristics from Philippe 2015) on per-lift e1RM, used as a readiness trend display rather than as a prescription engine.

### Gaps
- No head-to-head trials comparing app algorithms (e.g. MacroFactor vs Fitbod vs fixed programs) on outcomes were found.
- No validated optimal τ values for human resistance-training fatigue by muscle group were found.
