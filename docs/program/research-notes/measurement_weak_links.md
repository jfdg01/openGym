# Measuring strength progress across many exercises and detecting weak links

Evidence labels used throughout: **[VALIDATED]** = peer-reviewed data (systematic review, cohort or reliability study); **[PRACTITIONER]** = coaching or sports-science convention with no direct validation; **[FOLKLORE]** = popular claim with no traceable evidence. **[UNVERIFIED]** = I know of the claim but could not fetch a primary source in this session (PubMed, Europe PMC and ResearchGate were blocked or captcha-walled), so the report writer should treat it with care.

Research limits: PubMed E-utilities and Europe PMC were blocked by the egress proxy, and pmc.ncbi.nlm.nih.gov sometimes returned a captcha. The findings below come from pages I could actually fetch: Springer, BJSM, SAGE abstracts, sportsci.org, PMC (sometimes), and a university-hosted PDF.

## 1. Reliability, typical error and smallest worthwhile change of strength measures

### Takeaway
A true 1RM in a familiar exercise is very reliable at the group level (median ICC 0.97, median CV about 4%). Even so, about 4% of noise per test means one test against one test cannot reliably show a change smaller than about 8–10% for one person. Estimated 1RM (e1RM) from submaximal sets adds prediction error that grows with the number of reps. Isometric tests with cheap load cells or crane scales can have good reliability within a session but much worse reliability between sessions (neck: CV 15–20%).

### Cited Findings
- **1RM test–retest, systematic review (Grgic et al. 2020, Sports Med Open; 32 studies, n = 1,595)** [VALIDATED]: ICC 0.64–0.99, median 0.97; 92% of ICCs ≥ 0.90. CV 0.5–12.1%, median 4.2%. — [Grgic et al. 2020](https://link.springer.com/article/10.1186/s40798-020-00260-z)
  - With ≥ 1 familiarization session the median CV was 3.8%; with none it was 5.3%. The authors say familiarization is "not necessary" for reliability but advise it when technique is a safety concern. — [same](https://link.springer.com/article/10.1186/s40798-020-00260-z)
  - Upper body median CV 4.1%, lower body 4.7%. Participants with some training experience had a median CV of 3.3%, untrained ones 5.5%. — [same](https://link.springer.com/article/10.1186/s40798-020-00260-z)
  - Systematic learning effect: when the retest differed, it was higher, by a median of 5.5 kg for lower body (range 1.1–17.5 kg) and 1.8 kg for upper body (range 0.5–4.9 kg). — [same](https://link.springer.com/article/10.1186/s40798-020-00260-z)
  - Bland–Altman 95% limits of agreement: about ±3–5 kg bench press, ±5–8 kg power clean, ±8–13 kg leg press, ±10–15 kg squat. — [same](https://link.springer.com/article/10.1186/s40798-020-00260-z)
  - The review reports no SWC or MDC values. — [same](https://link.springer.com/article/10.1186/s40798-020-00260-z)
- **Smallest worthwhile change (Hopkins)** [PRACTITIONER, widely used in sports-science statistics]: for non-competition or team-sport measures the default SWC is 0.2 × the between-athlete SD (Cohen d = 0.2). For elite individual competition performance it is 0.3 × the athlete's within-athlete competition variability. Noise should be expressed as the typical error (TE) from a reliability study. "Most performance tests are noisier than the smallest worthwhile change." — [Hopkins 2004, Sportscience 8](https://www.sportsci.org/jour/04/wghtests.htm)
- **Isometric neck strength, load cell plus head harness (rugby union; SOUFEI SF-912, 20 Hz)** [VALIDATED, small sample]:
  - Within a session: ICC 0.86–0.95, CV 6.4–8.8% (flexion ICC 0.91 / CV 6.7%; extension ICC 0.86 / CV 8.8%).
  - Between sessions: ICC 0.51–0.69, CV 14.5–19.8%.
  - Flexion:extension ratio: CV 11.5% within a session, about 21–24% between sessions.
  - Typical error within a session: 1.6–2.5 kg. — [Reliability of Repeated Isometric Neck Strength in Rugby Union Players Using a Load Cell Device (PMC9031103)](https://pmc.ncbi.nlm.nih.gov/articles/PMC9031103)
- The authors used these bands: ICC < 0.40 poor, 0.40–0.75 fair, 0.75–0.90 good, > 0.90 excellent; CV ≤ 10% good, ≤ 20% acceptable. — [same](https://pmc.ncbi.nlm.nih.gov/articles/PMC9031103)
- Other field-based neck tests (between-session reliability) were studied by Birmingham City University in 2024 (*Sensors* 24:5015). I could not fetch numbers. — [Between-Session Reliability of Field-Based Assessments of Isometric Neck Strength](https://www.open-access.bcu.ac.uk/15729/)

### Inferences
- Rough individual noise threshold: Hopkins' rule for unusual change, when no SWC is defined, is about 2.0 × TE (section 3). For a 1RM or e1RM with a CV of about 4%, one session against one session needs a change of about **8%** before it is likely real. That is larger than the gains a trained lifter makes in a month or two. Single-session comparisons will therefore mostly be noise, and trend methods across many sessions are needed (section 3).
- Isometric tests with a crane or hanging scale behave like the neck study: good within a session, poor between sessions. To reduce noise, take the best or mean of 3 attempts and keep a fixed set-up (same anchor, joint angle and harness). The between-session CV of about 15% means only large changes (about 30%) are detectable test against test.
- For the app: store a per-exercise TE estimate. Start with a default (about 4% for barbell or machine e1RM, about 15% for improvised isometric tests). Replace it with the athlete's own residual SD once 10 or more data points exist (Hopkins' method, section 3).

### Gaps
- I could not fetch reliability data for handheld dynamometry (HHD) of the shoulder, hip or knee. HHD reliability is commonly reported as good to excellent within a tester when the device is fixed with a belt, and worse with a hand-held tester on strong muscles (tester-strength ceiling) [UNVERIFIED]. No CV or ICC numbers are verified here.
- I found no verified reliability data for crane-scale or hanging-scale isometric tests (the neck load-cell study is the closest analogue).
- No grip-strength reliability or norms were fetched. Dodds et al. 2014 (PLoS One) life-course centile curves are the standard UK reference [UNVERIFIED].
- I found no published MDC or SWC values for e1RM taken from everyday training sets.

## 2. Comparing progress across very different exercises, and estimating strength from high-rep sets

### Takeaway
1RM prediction from reps to failure is accurate up to about 5 reps, acceptable to about 10, and degrades steeply beyond that. Reynolds et al. recommend no more than 10 reps in linear equations. Self-reported RIR adds about 1 rep of error, and much more when more than 12 reps remain. For exercises trained at 12–30 reps, track performance in the native rep bracket (load at a fixed rep target, or reps at a fixed load) instead of converting to a 1RM. Compare exercises by percent change against their own noise (a z-score in TE units), not by absolute or bodyweight-relative numbers.

### Cited Findings
- **Reynolds et al. 2006, JSCR (n = 70 plus 20 cross-validation; leg press and chest press)** [VALIDATED]: — [Reynolds et al. 2006 PDF](https://www.unm.edu/~rrobergs/478RMStrengthPrediction.pdf)

  | Predictor | Leg press R² | Leg press SEE | Chest press R² | Chest press SEE |
  |---|---|---|---|---|
  | 5RM | 0.974 | 16.2 kg | 0.993 | 3.0 kg |
  | 10RM | 0.933 | 26.1 kg | 0.976 | 5.4 kg |
  | 20RM | 0.915 | 29.4 kg | 0.955 | 7.4 kg |

  - Cross-validation SEE, leg press: 13.5, 23.8 and 33.1 kg. Chest press: 1.8, 3.6 and 4.8 kg (for 5RM, 10RM and 20RM).
  - The authors state that accuracy worsens "with increasing repetitions to failure" and recommend no more than 10 reps in linear 1RM equations.
- **A 2024 cross-validation of 1RM equations from reps to failure for bench press and leg extension** exists (JSCR, PubMed 39495260). I could not fetch details. — [PubMed 39495260](https://pubmed.ncbi.nlm.nih.gov/39495260/)
- **A weight-dependent 1RM prediction equation optimized on large datasets** is available as a SportRxiv preprint. It argues that fixed formulas such as Epley and Brzycki are biased across load ranges. I could not fetch details; it is not peer-reviewed. — [SportRxiv preprint 768](https://sportrxiv.org/index.php/server/preprint/download/768/1661)
- **Accuracy of predicting reps to failure (Halperin et al. 2022, Sports Med; 12 studies, n = 414)** [VALIDATED, exploratory meta-analysis]: — [Halperin et al. 2022](https://link.springer.com/article/10.1007/s40279-021-01559-x)
  - Pooled error: people underpredict reps to failure by **0.95 reps** (95% CI 0.17–1.73); I² = 97.9%; between-person SD 1.45 reps.
  - Error grows with reps remaining: slope β = 0.06 for sets with ≤ 12 reps to failure versus **β = 0.47 for sets with > 12 reps to failure**. Each extra rep beyond 12 adds about half a rep of error.
  - Training status had no meaningful effect. Later sets were slightly more accurate (trivial effect). Upper versus lower body made no difference.
- Remmert, Laurson and Zourdos 2023 (*Perceptual and Motor Skills*) compared intraset RIR accuracy in single-joint and multi-joint exercises, in trained and untrained men and women. Only the title was retrieved. — [Remmert et al. 2023](https://journals.sagepub.com/doi/abs/10.1177/00315125231169868)

### Inferences
- **Standardized e1RM:** compute e1RM = f(load, reps + RIR) only for sets with reps + RIR ≤ about 10–12. For longer sets, keep a separate "rep-bracket" metric for each exercise, for example the best load × (reps + RIR) within 12–20 or 20–30. Compare that exercise only with its own history in the same bracket. Mixing brackets breaks comparability, because equations are biased at high reps and RIR error inflates (about 0.5 reps per rep beyond 12).
- **Cross-exercise comparison:** express each exercise's change as (current − baseline) ÷ baseline, then divide by that exercise's TE (a signal-to-noise z-score). This puts a noisy isometric test and a stable barbell lift on one scale for ranking "weakest progress".
  - Bodyweight-relative numbers and population standards answer a different question (absolute level, not progress). They should not be the main ranking metric.
- **Time-based isometric holds** (seconds to failure) are endurance measures. Hold time does not change linearly with force, so a 20% longer hold is not 20% more strength. Prefer force-based isometrics (scale or load cell) or a loaded hold at a fixed time.
- **Unilateral work:** log left and right separately and compute e1RM for each side. The left/right ratio then becomes a ratio metric (section 4).

### Gaps
- I found no verified validity data for converting 12–30-rep sets into 1RM in trained lifters, beyond the Reynolds 20RM data.
- No published comparison of z-score versus percent-change methods for ranking exercises within one person was found.
- I fetched no strength-standards datasets (Strength Level, OpenPowerlifting). They are crowd-sourced or competition-selected and useful only as rough context [PRACTITIONER].

## 3. Detecting trends in noisy individual data, and how many sessions are needed

### Takeaway
The best-documented approach for one athlete is Hopkins' individual-trend method:
- Fit a linear regression over the chosen time window.
- Take noise from a reliability study, or from the athlete's own residual SD when there are 10 or more tests.
- Flag a point or trend only when it falls outside a band of "trivial change plus uncertainty". Without a defined SWC, the default flag is a change of about 2 × TE.
- Compare the slope against a target "smallest important trend" (desired change ÷ time).

This replaces a fixed baseline with a rolling regression and gives a principled rule for declaring a stall.

### Cited Findings
- **Hopkins 2017, "Spreadsheets for monitoring an individual's changes and trend"** [PRACTITIONER / sports-science methods, widely used]: — [Hopkins 2017](https://sportsci.org/2017/wghtrend.htm)
  - Uses a linear trend through the chosen tests (no quadratic fit is described).
  - TE comes from a short-term reliability study. Otherwise it is the trend's standard error of the estimate (SEE), which "needs at least 10 tests" to be reasonably precise and overestimates noise if real changes occurred.
  - Averaging n repeat trials divides TE by √n. Athletes' SEEs can be pooled by averaging their squares, weighted by degrees of freedom.
  - A score is flagged when it falls outside the trivial-change zone around the trend line, meaning the true deviation is likely (> 75%) substantial. "Very likely" means > 90%. A result is "unclear" if it could be both substantially positive and substantially negative, with a 10% default for "could".
  - Target trend: desired change ÷ period. This becomes the smallest important trend, and the fitted slope is tested against it.
  - With no SWC defined, flag changes larger than about 2.0 × TE (t × √2 × TE at a cumulative probability of 0.9).
  - A measure is noisy when TE > ½ SWC; many small changes will then stay unclear. Simulate Type I and Type II error rates before relying on the flags.
- Hopkins 2004: report chances that a true change is beneficial, trivial or harmful; partly discount unrealistically large changes from noisy tests. — [Hopkins 2004](https://www.sportsci.org/jour/04/wghtests.htm)
- Green et al. 2020 (BJSM, hamstring injury risk factors) note that strength qualities change over time, so a single baseline measure may not validly predict later outcomes. This indirectly supports rolling rather than fixed baselines. — [Green et al. 2020, BJSM](https://bjsm.bmj.com/content/54/18/1081)

### Inferences
Inferences for an implementation:
- **Rolling best vs rolling mean:** a rolling maximum of e1RM is biased upward by noise and only ratchets up, so it cannot show a decline. A rolling mean or median of each session's best-set e1RM is unbiased but lags. A robust regression slope over the last N sessions (Theil–Sen, or ordinary least squares with residual SD as TE) gives both direction and a confidence interval and matches Hopkins' method.
- **Sessions needed:** Hopkins needs ≥ 10 tests to estimate SEE well.
  - Rough worked example with a session-to-session CV of 4%: the standard error of an OLS slope over n equally spaced sessions is σ / √(Σ(t − t̄)²). For 8 weekly sessions, Σ(t − t̄)² = 42, so SE ≈ 4% / 6.5 ≈ 0.6% per week, and a 95% CI is about ±1.2% per week.
  - That is about the size of a novice-to-intermediate weekly gain. A stall (slope ≈ 0) can be distinguished from about 1% per week of progress only after roughly 8–12 data points. With 1–2 sessions per week per exercise, that means a window of about 6–12 weeks.
  - This arithmetic is mine and not from a source; the window sizes are assumptions to tune.
- **Statistical process control (SPC):** Shewhart-style limits (mean ± 2–3 SD of the residuals) and CUSUM or EWMA charts are standard industrial methods. In this setting they are equivalent in spirit to Hopkins' 2 × TE rule. CUSUM or EWMA would catch small sustained drifts sooner than point-by-point checks. Their use for strength logs is [PRACTITIONER / extrapolation]; no strength-training validation was found.
- **Bayesian or n-of-1 models:** a hierarchical model, with exercises nested within the athlete, could shrink noisy exercise slopes toward the athlete's mean slope. That is useful with about 100 exercises and few data points each. No strength-specific validation was found [extrapolation].
- **Weak-link rule (proposal):** flag an exercise when its slope over the last 6–12 weeks is "likely" (> 75%) below the target trend, or below zero. Rank weak links by the z-score of the slope, not the raw slope.

### Gaps
- I found no peer-reviewed study of how many sessions are needed to detect a strength plateau in one lifter using training-log e1RM.
- No validation was found for SPC, CUSUM or Bayesian hierarchical methods applied to individual resistance-training logs.

## 4. Reference strength ratios: what has evidence and what does not

### Takeaway
The evidence for ratios as injury predictors is weaker than their popularity suggests:
- **Hamstring:quadriceps:** a 2020 meta-analysis (78 studies) found isokinetic testing (where H:Q comes from) unrelated to hamstring injury risk in 11 meta-analyses.
- **Shoulder:** in professional pitchers, preseason ER weakness and the ER:IR ratio are associated with shoulder or throwing injury.
- **Neck:** the flexion:extension ratio is about 0.7–0.8 in rugby players but has no agreed cut-off.
- **Poliquin-style structural balance ratios** (for example, front squat = 85% of back squat) are coaching conventions with no peer-reviewed validation found.
- Ratios from free-weight or cable e1RMs are not interchangeable with isokinetic torque ratios.

### Cited Findings
- **Hamstring:quadriceps ratio and hamstring injury (Green, Bourne, van Dyk and Pizzari 2020, BJSM; 78 studies, 8,319 hamstring strain injuries, 71,324 athletes)** [VALIDATED]: — [Green et al. 2020](https://bjsm.bmj.com/content/54/18/1081)
  - "In 11 meta-analyses isokinetic testing was unrelated to HSI risk."
  - None of the 13 strength-related variables meta-analyzed was significantly associated.
  - Nordic hamstring strength: SMD −0.31 (95% CI −0.97 to 0.4).
  - Limited evidence linked low strength endurance (single-leg hamstring bridge) and HHD strength to injury.
  - Conventional H:Q appears only in a figure.
- **Shoulder ER:IR in professional baseball pitchers (Byram et al. 2010, AJSM; prospective, one organization, 2001–2005)** [VALIDATED, one cohort, correlational]: — [Byram et al. 2010](https://journals.sagepub.com/doi/10.1177/0363546509360404)
  - Prone ER:IR ratio associated with shoulder injury (P = .037), borderline for throwing injury overall (P = .051).
  - Prone ER (P = .003), seated ER (P = .048) and supraspinatus strength (P = .006) associated with throwing injury needing surgery.
  - No associations in players with prior surgery.
  - Conclusion: "Preseason weakness of external rotation and SS strength is associated with in-season throwing-related injury resulting in surgical intervention."
- Other baseball ER/IR work: player type and region affect ER/IR strength ([Int J Sports Phys Ther 2021](https://ijspt.scholasticahq.com/article/25237-professional-baseball-player-type-and-geographic-region-of-origin-impacts-shoulder-external-and-internal-rotation-strength)); dominant-arm ER/IR strength relates to arm pain in youth players ([IJSPT](https://ijspt.scholasticahq.com/article/124447-dominant-arm-internal-and-external-rotation-strength-is-related-to-arm-pain-in-youth-baseball-players)). Titles only.
- **Neck flexion:extension and left:right** [VALIDATED descriptive, no thresholds]: — [PMC9031103](https://pmc.ncbi.nlm.nih.gov/articles/PMC9031103)
  - Rugby players: extension 31.9 ± 5.6 kg, flexion 23.9 ± 4.7 kg.
  - Flexion:extension 0.77–0.82 within a session, 0.70–0.78 between sessions. Left:right 0.97–1.04.
  - A cited review gives flexion:extension of 0.56 for forwards and 0.61 for backs.
  - The authors say there is "no agreement on the strength testing method to be used or requisite strength levels." Flexion:extension imbalance is linked to higher head accelerations in other cohorts (soccer heading), with no cut-off.
  - The ratio itself had a between-session CV of about 21–24%, much noisier than its components.
- **Limb symmetry index (LSI)** [VALIDATED critique]: Wellsandt, Failla and Snyder-Mackler 2017 (JOSPT 47(5):334–338), "Limb Symmetry Indexes Can Overestimate Knee Function After Anterior Cruciate Ligament Injury". When the uninjured limb also weakens, LSI ≥ 90% can hide deficits. The proposed alternative compares against an estimated pre-injury capacity (EPIC). — [PubMed 28355978](https://pubmed.ncbi.nlm.nih.gov/28355978/); [Aspetar Journal commentary](https://journal.aspetar.com/en/journals/volume-9-targeted-topic-return-to-performance-after-acl-reconstruction/is-it-time-to-change-how-we-assess-functional-performance-following-acl-reconstruction)
  - The full text was captcha-walled; exact counts were not verified.
- **Poliquin / structural-balance ratios** [PRACTITIONER / FOLKLORE]: the Thibarmy article lists, for example (no studies cited): — [Thibaudeau, "Know Your Ratios"](https://thibarmy.com/know-your-ratios-destroy-weaknesses/)
  - Against bench press: close-grip bench 90%, incline bench 80%, strict military press 60%, weighted dip (including bodyweight) 105%, supinated chin-up (including bodyweight) 90%, chest-supported row 70%, preacher curl 40%.
  - Against back squat: front squat 85%, deadlift 120%, bench press 75%.
  - The ratios are said to be "adapted from Poliquin's Structural Balance material and Russian Olympic weightlifting literature" plus powerlifting world records.
  - Other practitioner pages ([Peter Roberts](http://www.peterrobertscoaching.com/blog/definitive-guide-to-structural-balance-training), [Iron Forge](https://www.ironforgegym.co.uk/article/structural-balance-and-accessory-work/), [BFS PDF](http://office.biggerfasterstronger.com/uploads2/10_JulAug_StructuralBalanceAndAuxExercises.pdf)) repeat the concept. A search found no peer-reviewed validation.

### Inferences
- **Ratios worth implementing:**
  1. **Left:right on the same unilateral exercise.** Same movement, same day, the noise largely cancels. A practical flag is < 90% (the LSI convention), confirmed over several sessions. Given an e1RM CV of about 4% per side, a single-session ratio can vary by about ±6% by noise alone (√2 × 4%), so require a persistent deficit.
  2. **ER:IR from comparable cable or band rotations at the same arm position.**
  3. **Neck flexion:extension**, as descriptive only.
- **Thresholds:**
  - H:Q (conventional about 0.6; functional eccentric-hamstring : concentric-quadriceps about 1.0) and hip adduction:abduction (about 80%) are commonly quoted [UNVERIFIED in this session; injury-prediction value weak for H:Q per Green 2020].
  - Treat them as soft "look here" hints, not targets.
- **Ratios from free weights or cables vs isokinetic torque:** isokinetic norms are joint torque at a set velocity with a fixed axis. Gym e1RMs depend on lever arms, cable cam profiles, stabilizer demands and technique. A leg-curl:leg-extension ratio from machine weights is not comparable to isokinetic H:Q norms. Use only self-referenced trends of such ratios (is the ratio drifting?), not absolute comparisons with clinical norms.
- **Ratios are noisier than their parts:** the variances of the two components add (neck ratio CV of about 21–24% between sessions). A ratio-based weak link needs more data points than a single-exercise trend.

### Gaps
- Not verified in this session (search was blocked):
  - Tyler et al. 2001 hip adduction:abduction < 80% and groin strain in NHL players [UNVERIFIED].
  - Croisier et al. 2008 isokinetic H:Q and hamstring strain in soccer [UNVERIFIED].
  - Isokinetic ER:IR norms of about 0.66–0.75 [UNVERIFIED].
  - Grip-strength norms, Dodds 2014 [UNVERIFIED].
- No study was found that validates ER:IR or H:Q computed from free-weight or cable loads against isokinetic dynamometry.
- No neck flexion:extension injury threshold exists in the fetched literature.

## 5. Alternatives to a fixed baseline

### Takeaway
A fixed baseline at the end of a return-to-training ramp can be replaced by a **rolling regression window** (Hopkins' trend method, 6–12 weeks) together with an **all-time-best reference** and an explicit **target trend**. The trend is the main signal. The all-time best (or the LSI-style "estimated pre-injury capacity" idea from ACL rehab) answers "have I recovered previous capacity?". Population standards are context only.

### Cited Findings
- Hopkins' trend approach uses a chosen window of tests and a "target trend" (desired change ÷ period) instead of a single baseline. Noise is estimated from the athlete's own residuals once there are 10 or more tests. — [Hopkins 2017](https://sportsci.org/2017/wghtrend.htm)
- LSI literature shows that comparing against a contemporaneous reference that can itself decline (the uninjured limb) can overestimate function. The proposed alternative is an estimated pre-injury capacity. — [Wellsandt et al. 2017, PubMed 28355978](https://pubmed.ncbi.nlm.nih.gov/28355978/)
- Strength qualities change over time, so single baseline measures have limited predictive validity. — [Green et al. 2020](https://bjsm.bmj.com/content/54/18/1081)
- Systematic retest learning effects: the second 1RM test was a median 5.5 kg (lower body) or 1.8 kg (upper body) higher. A baseline set during the first exposures to an exercise is therefore biased low and inflates early "gains". — [Grgic et al. 2020](https://link.springer.com/article/10.1186/s40798-020-00260-z)

### Inferences
- **Options**, ranked for simplicity and validity:
  1. **Rolling-window slope** over the last 6–12 weeks against the target trend. No baseline event is needed.
  2. **Percent of own best e1RM** in the last 12 months. This is an EPIC-like "recovered capacity" metric, useful after layoffs.
  3. **First stable window:** the median of the first 3–4 sessions after the ramp, discarding the first 1–2 exposures to cancel the learning effect.
  4. **Population standards** (Strength Level, OpenPowerlifting-derived): only as context for absolute weak links. They exist mostly for the main barbell lifts and are self-selected samples.
- Dropping the ramp-end event: option 1 needs no special event. Any layoff simply shows up as a negative deviation, and the ramp becomes part of the trend.

### Gaps
- No peer-reviewed comparison of fixed versus rolling baselines for monitoring strength in individuals was found.
