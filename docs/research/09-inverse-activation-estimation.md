# 09 — Inverse Methods for Estimating Muscle Activation from Observed Motion

Task: T-031 (Phase 1b, inference research). Question: can muscle activation be legitimately
back-solved from how a golf swing visually looks (motion alone, or motion + limited EMG),
and with what validated error bounds? Status: DONE 2026-08-07 — 19 sources. Sources below are
cited by URL/PMID/DOI as fetched; nothing is entered without its own citation. Two open gaps
declared in §9 (Crowninshield & Brand 1981 primary quantitative detail; ballistic-throwing-sport
SO-vs-EMG study) for a future targeted follow-up if the project revisits this file.

---

## 1. Inverse dynamics — computing net joint moments from motion + GRF

Inverse dynamics (ID) is the first, mandatory step before any muscle-level back-solving: it
converts measured segment kinematics (positions/accelerations) plus ground reaction force (GRF)
into **net joint moments** using the Newton-Euler equations, segment-by-segment, working from
the distal end (where GRF is applied) proximally. It does NOT resolve individual muscle forces —
that is what static optimisation/CMC/EMG-driven methods do on top of the ID output.

Camomilla, Bergamini, Fantozzi & Vannozzi 2017, "Methodological factors affecting joint moments
estimation in clinical gait analysis: a systematic review" (*Biomed Eng Online* 16:106,
PMID 28821242, PMC5563001), synthesising 67 studies, is the most rigorous source found on ID
error propagation:
- Four error categories: (a) kinematic measurement/processing (marker noise, soft-tissue
  artefact, anatomical landmark identification), (b) GRF measurement, (c) joint model parameters
  (joint-centre/axis location), (d) body-segment inertial parameters (BSIP).
- Quantified magnitudes: knee-coordinate perturbations → net knee-moment errors of **200–1500
  Nm/m** (≈0.2–1.2% BW×height); a **30 mm hip-joint-centre mislocation → ≈−22% error in
  flexion-extension moment and ≈−15% in abduction-adduction moment**; a 0.01 m centre-of-pressure
  (GRF) error → **≈14% change in maximum joint torques**; BSIP variation → up to **20% difference
  at the hip during fast cadence** (BSIP error is otherwise "negligible" at normal cadence — i.e.
  it stops being negligible precisely as speed increases).
- Dominant error sources: kinematic processing and joint-centre/axis uncertainty exceed BSIP
  contributions in most conditions.
- **Directly relevant warning for a golf-swing application**: "uncertainties on joint moments
  increase with increasing velocities," effects are "substantially larger during swing phases
  versus stance" (i.e. worse for the ballistic, non-GRF-instrumented portion of a motion), and
  errors scale worse for **proximal joints** (hip, spine — exactly the segments most implicated
  in golf trunk/pelvis rotation). The authors explicitly caution against **"extending the results
  found for walking and stair ascending/descending… in case of activities involving higher
  accelerations"** — i.e. their own error bounds, already sizeable, are not validated for
  anything as fast as a golf downswing and the authors say so themselves.
- GRF necessity: the review notes that omitting GRF/inertial terms (e.g. treating a phase as
  quasi-static) is valid **only when the inertial contribution is minor** — true for slow tasks,
  false for a task with the segment accelerations of a golf downswing. It also flags that most
  of the field simply treats force-plate GRF as "virtually error-free," which the review
  identifies as an unexamined assumption, not a validated one.

**Conclusion for section 1**: ID itself is well-established and its main error sources are
quantified — but every one of those quantified error studies was done on walking or comparably
slow tasks, and the review's own authors state the errors are known to grow with velocity and
acceleration and refuse to extrapolate their bounds to fast movements. No equivalent
quantification exists (found in this search) for a task at golf-downswing speed.

## 2. The muscle redundancy problem

Formally: at any instant, the ID step yields a small number of net joint moments (a handful of
degrees of freedom — e.g. a leg model has roughly hip [3 DOF] + knee [1] + ankle [2] = 6), but
the number of muscles capable of producing those moments is far larger — Michaud et al. 2021
(§3 below) used a **43-muscle model of a single leg**. Any single joint moment can be produced by
countless combinations of agonist/antagonist/synergist forces (differing co-contraction levels,
differing load-sharing between muscles crossing the same joint) that all sum to the same net
moment. The system of equations (moments = f(muscle forces)) is therefore **under-determined**:
more unknowns (muscle forces/activations) than equations (joint moments), so **without additional
constraints there are infinitely many activation vectors consistent with one observed motion**.
This is the mathematical core of why back-solving activation from motion alone cannot, in
principle, have a single "correct" answer — it requires an extra, non-motion-derived assumption
(a cost function, or measured EMG, or synergy structure) to pick one candidate out of an infinite
set, and different reasonable-looking assumptions pick different candidates (§3/§4 quantify how
much those candidates disagree with what muscles actually do).

A second, deeper layer of non-uniqueness, distinct from the mathematical indeterminacy above:
Latash 2012, "The bliss (not the problem) of motor abundance (not redundancy)" (*Exp Brain Res*
217(1):1-5, doi:10.1007/s00221-012-3000-4, PMID 22246105), reviewing ~10 years of motor-control
literature built on Bernstein's original formulation of the degrees-of-freedom problem, argues
the field's traditional framing (redundancy = a problem to be "eliminated" by picking one optimal
solution) is itself likely wrong: real neuromotor control appears to actively exploit "good
variance" — task-irrelevant variability across repetitions — rather than converging on one fixed
activation pattern each time. If correct, this means even the same golfer, swinging the same club
the same way twice, may not use the same muscle activation solution both times even though the
resulting motion looks visually identical — a second, biological source of non-uniqueness on top
of the mathematical one, and one that no cost-function optimisation is designed to capture at all
(optimisation methods deliberately return one single "best" answer, precisely the opposite of
what this literature says the real neuromuscular system does).

**Consequence for the golf-swing back-solving question**: even a perfect inverse-dynamics
solution (perfect kinematics + perfect GRF) does not converge on a unique muscle activation
pattern. Any back-solved activation map is necessarily *a* solution consistent with an assumption
external to the motion (cost function, EMG constraint, synergy model) — never *the* solution,
and there is motor-control-literature reason to doubt a single "the" solution exists at all for
a given visual motion, even in principle.

## 3. Static optimisation — cost functions and quantitative EMG validation

Static optimisation (SO) resolves the muscle redundancy problem at each time instant by
minimising a cost function (commonly sum of squared muscle forces, squared relative forces,
squared stresses, or a min-max criterion) subject to the constraint that net muscle moments
reproduce the joint moments from inverse dynamics. It has existed for decades but "none have
successfully transitioned into clinical practice… due to lack of validation" (Erdemir et al.
2007, *Clin Biomech* 22(2):131-154, doi:10.1016/j.clinbiomech.2006.09.005, PMID 17070969).

**Quantitative validation found (gait, the best-studied case):**
- Michaud, Lamas, Lugrís & Cuadrado 2021 (*J Neuroeng Rehabil* 18:17, PMID 33509205, PMC7841909),
  10 healthy subjects, 43-muscle Hill-type lower-limb model, 4 SO cost functions vs surface EMG
  during gait. Best-performing criterion (sum of squared muscle forces): **mean r = 0.74 across
  all muscles**. Per-muscle Pearson r: gluteus maximus 0.89, gastrocnemius medialis 0.86, biceps
  femoris 0.78, gastrocnemius lateralis 0.75, gluteus medius 0.71, vastus medialis 0.68, vastus
  lateralis 0.68, semitendinosus 0.68, **tibialis anterior 0.61 (weakest)**. Worst criterion
  (minimise largest relative muscle force) also bottomed at r = 0.61. No RMSE reported. No
  significant difference between best two criteria at group level, but per-muscle spread is
  large (0.61–0.89) even in this best-case scenario (slow, cyclic, thoroughly characterised gait).
- Heintz & Gutierrez-Farewik 2007 (*Gait Posture* 26(2):279-88, doi:10.1016/j.gaitpost.2006.09.074,
  PMID 17071088): SO vs EMG-to-force processing during gait — "reasonably good correlation in
  the plantarflexor and dorsiflexor muscles" but "**less correlation in the knee flexor and
  extensor muscles**" (biarticular muscles crossing hip+knee or knee+ankle fare worse than
  monoarticular ones). No numeric r/RMSE surfaced in the abstract.
- Rauber, Lüscher, Poux et al. 2024 (*J Biomech* 163:111922, doi:10.1016/j.jbiomech.2023.111922,
  PMID 38220500), paraspinal muscles, SO validated against EMG: cross-correlation **≥0.97 for
  mild-deformity, quasi-static object-lifting** (best case) collapsing to **XCorr 0.51 with high
  RMSE for moderate spinal deformity and for walking/running** (dynamic tasks). Authors'
  conclusion, quoted directly: **"Static optimization alone seems not appropriate for predicting
  muscle activity… particularly… when performing upright activities such as walking and
  running."** This is the clearest published statement that SO accuracy degrades specifically
  as a task becomes more dynamic — directly relevant to a 0.25 s ballistic golf downswing, which
  is far more dynamic than walking or running.

**Pattern across all three studies:** SO's best-case agreement with EMG (r ≈ 0.74–0.97) occurs
for slow, cyclic, well-characterised, near-optimal tasks (steady gait, quasi-static lifting).
Agreement degrades (r/XCorr down to ≈0.5–0.6) for (a) biarticular muscles, (b) faster/more
dynamic tasks, and (c) any subject/movement whose control deviates from the optimality
assumption the cost function encodes. No source reviewed reports SO validation on a task
remotely as fast as a golf downswing.

## 4. Computed muscle control / dynamic optimisation — validation

Afschrift, Kistemaker, Bobbert & De Groote 2025, "Benchmarking the predictive capability of
human gait simulations" (*PLoS Comput Biol*, PMID 41248112, PMC12622833) is not CMC per se but
the closest available rigorous benchmark of a full predictive/dynamic-optimisation musculoskeletal
pipeline (31-DOF, 92-muscle Hill-type model, direct-collocation optimal control minimising a
multi-objective cost of metabolic power + activation + joint acceleration + passive torque).
Findings directly bear on trusting dynamic optimisation outside its tuned regime:
- Metabolic power prediction: R² = 0.91 overall but with **systematic 15% underestimation**;
  worse under incline (27% underestimation) — i.e. error grows with mechanical demand.
- Joint kinematics were captured "reasonably well" only for **0.7–1.6 m/s**; the model **failed
  qualitatively at the walk-to-run transition (≥1.8 m/s)**, spontaneously switching to a grounded
  running gait not seen experimentally at that speed — a categorical failure mode, not just
  growing numerical error, right at a much smaller speed jump than walking→golf-downswing.
- Cost-function weights were fitted by "trial-and-error… based on the realism of the simulated
  walking pattern at 1.3 m/s only" — the authors explicitly flag "considerable risk of
  overfitting" and that unmeasurable model/energetics errors can be masked by re-tuning the cost
  function to look plausible, i.e. a plausible-looking output does not certify the activation
  solution is correct.
- Authors' own conclusion: confident extrapolation requires improved models of "musculoskeletal
  mechanics, energetics, passive elastic structures, and neural control" — i.e. current dynamic
  optimisation is not yet trusted even by its own practitioners outside level walking.

**CMC validation with true in-vivo ground truth (rare):** Thelen, Choi & Schmitz 2014,
"Co-simulation of neuromuscular dynamics and knee mechanics during human walking" (*J Biomech
Eng*, PMID 24390129, PMC4023657, DOI 10.1115/1.4026358) used computed muscle control to drive a
musculoskeletal model to track measured knee kinematics in a subject with an **instrumented knee
replacement** (i.e. actual in-vivo joint contact force, not just EMG, as ground truth) — one of
the only studies anywhere with true internal-force validation:
- Peak medial contact force predicted within **4%** of measured; peak total contact force within
  **17%**; RMSE **0.26 BW (medial), 0.42 BW (lateral), 0.51 BW (total)**.
- EMG comparison: "reasonably good temporal agreement" for vastus lateralis, medial
  gastrocnemius, soleus, tibialis anterior — but **discrepancies in hamstrings and rectus
  femoris**, i.e. the biarticular muscles again fare worse, consistent with the biarticular
  under-prediction pattern in §3.
- Task: level walking. No ballistic/fast-task CMC validation with in-vivo force ground truth was
  located.

**Ballistic-task-adjacent validation (hopping — the closest available fast/elastic task):**
Jessup, Kelly, Cresswell & Lichtwark 2023, "Validation of a musculoskeletal model for simulating
muscle mechanics and energetics during diverse human hopping tasks" (*R Soc Open Sci*,
PMID 37885982, PMC10598413, DOI 10.1098/rsos.230393), used OpenSim Moco (default cost function:
minimise sum of squared controls) across light/medium/heavy hopping conditions, validated against
EMG for 7 muscles:
- Group-level R² for peak activation: **vastus lateralis 0.97** (best) down to
  **tibialis anterior 0.02** (essentially uncorrelated) — soleus 0.60, biceps femoris 0.45,
  gastrocnemius lateralis 0.36, rectus femoris 0.27, gastrocnemius medialis 0.22.
- Individual-level R² (i.e. per-subject, not pooled): worse across the board — VL 0.87 down to
  TA 0.11.
- "The inverse solutions… preferentially activated and handled uni-articular, extensor muscles
  best, compared to bi-articular and/or flexor muscles" — the third independent confirmation
  (after Heintz 2007 and Thelen 2014 above) of the biarticular-muscle failure mode.
- Correlations **"tended to weaken across hop frequencies"** — i.e. accuracy degrades as the task
  becomes more ballistic/higher-frequency, in the one study located that varies task speed while
  holding the modelling method fixed.
- Authors' own caution, directly on point for a single golf swing (an "individual-level," one-off
  event, not a group-averaged repeated cyclic task): **"current modelling approaches may be
  sufficient for predicting relative differences… on a group-level, but caution is required for
  interpretation of simulation outputs for individuals."**

**Synthesis of §3/§4/§6 quantitative findings** (all r/R² values found in this research pass,
ordered worst to best): TA in hopping R²=0.02 (individual 0.11) < paraspinal walk/run
XCorr=0.51 < TA in gait r=0.61 < RF/GM in hopping R²≈0.22–0.27 < VM/VL in gait r≈0.68 <
BF in hopping R²=0.45 < BF in gait r=0.78 < mean gait r=0.74 (Michaud, all muscles pooled) <
SOL in hopping R²=0.60 < GM (gastroc) in gait r=0.86 < GMax in gait r=0.89 < VL in hopping
R²=0.97 (best) < paraspinal quasi-static lifting XCorr≥0.97 (best). No single number is "the"
accuracy of static optimisation — it spans from essentially uncorrelated to near-perfect
depending on muscle, task, and whether the analysis is group- or individual-level, with a
consistent direction of degradation as tasks become faster/more individual/more biarticular.

## 5. EMG-driven and EMG-informed hybrid models

Princelle, Viceconti & Davico 2025, "EMG-Informed Neuromusculoskeletal Simulations Increase the
Accuracy of the Estimation of Knee Joint Contact Forces During Sub-optimal Level Walking"
(*Ann Biomed Eng*, PMID 40128488, PMC12075340):
- EMG-assisted vs pure static-optimisation stance-phase RMSE: **286.1 N (SO) vs 260 N
  (EMG-assisted) — roughly a 9% RMSE reduction** from adding EMG.
- Whole-cycle R²: both methods > 0.82; EMG-assisted only "marginally but consistently" better
  (13/15 trials) — i.e. **for near-normal movement the EMG advantage is small**.
- The advantage becomes large specifically for **"severely sub-optimal" control** — subjects
  whose real muscle recruitment departs from the cost function's optimality assumption (here,
  atypical knee-force profiles, missing/blunted force peaks, plausibly from fear-of-falling or
  weakness). Quoted: "the only viable solution so far is to resort to surface EMG data" for
  these cases, because **"the static optimization method… did not capture such abnormalities,
  resulting in typical knee joint contact force profiles"** — SO forces the answer toward what
  is optimal, not what the person actually did.
- This is the single most important structural finding for the golf-swing question: a fast,
  skill-dependent, individually idiosyncratic movement like a golf downswing is exactly the kind
  of "sub-optimal / atypical relative to a generic cost function" scenario where SO is documented
  to fail and where measured EMG becomes not just an accuracy improvement but a near-necessity
  for the muscles it's available for.
- Caveat: study is confined to level walking in elderly knee-implant patients; no statement
  about generalising to ballistic/golf-type movement (noted as an explicit limitation to avoid
  over-claiming here).

## 6. Failure modes — co-contraction, biarticular muscles, ballistic movements

Findings so far (co-contraction/antagonist-specific literature search yielded no direct hits in
this pass — logged as an open gap for a further targeted search):
- **Biarticular muscles fare worse than monoarticular ones** under SO — Heintz &
  Gutierrez-Farewik 2007 above (knee flexors/extensors crossing two joints predicted less well
  than uniarticular ankle plantar/dorsiflexors).
- **SO systematically reverts atypical/idiosyncratic activation toward the generic optimum** —
  Princelle et al. 2025 above: this is structurally identical to a co-contraction/antagonist
  under-prediction failure mode, since most standard SO cost functions (sum of squared
  forces/stresses) have no mechanism to reward antagonist co-activation — co-contraction is
  metabolically "expensive" under nearly every such cost function, so an SO solution will always
  minimise it unless the cost function is specifically constructed (or EMG-constrained) to allow
  it. This is inference from the mechanics of the optimisation, not a direct quoted statement,
  and is flagged as such.
- **Dynamic/fast-task degradation is directly evidenced**: Rauber et al. 2024 above (walking/
  running XCorr collapses to 0.51 vs ≥0.97 for quasi-static lifting) and Afschrift et al. 2025
  above (categorical gait-pattern failure at the walk-run transition, ≥1.8 m/s, well below any
  golf-swing-comparable speed).
- No source located yet that states a numeric error bound for movements in the ballistic,
  <0.3 s timescale of a golf downswing specifically — flagged as an unresolved gap pending
  further search of sport-ballistics literature (e.g. throwing, pitching, kicking).

## 7. Golf-swing-specific applications

**Musculoskeletal/muscle-level modelling of the golf swing essentially does not exist in the
peer-reviewed literature.** Search evidence for this negative finding:
- Bourgain, Rouch, Rouillon, Thoreux & Sauret 2022, "Golf Swing Biomechanics: A Systematic
  Review" (*Sports* 10(6):91, PMID 35736831, PMC9227529), reviewing **92 articles**, is confined
  entirely to kinematics (X-factor, crunch factor, swing plane, clubhead trajectory, kinematic
  sequence, joint angular kinematics). **No mention anywhere in the abstract of musculoskeletal
  modelling, static optimisation, muscle-force/activation estimation, EMG, or inverse-dynamics
  muscle-level approaches** — the review's own scope confirms this branch of golf research is
  essentially absent, and it explicitly flags "lack of methodological consensus" and
  under-adoption of ISB kinematic-reporting standards even at the kinematics level, i.e. the
  more basic layer beneath muscle-level work is itself immature.
- A targeted Europe PMC full-text search for `golf swing EMG-driven OR "muscle-driven
  simulation" AND golf` returned **zero results**. Absence of a hit is not proof of absence, but
  combined with the systematic review above it is reasonably strong evidence.
- **Nesbit & colleagues' golf forward-dynamics work is the closest existing golf-specific
  modelling, and it is explicitly torque-driven, not muscle-driven.** Nesbit 2005, "A three
  dimensional kinematic and kinetic study of the golf swing" (*J Sports Sci Med*, PMID 24627665,
  PMC3899667) and Nesbit & Serrano 2005, "Work and power analysis of the golf swing" (PMID
  24627666, PMC3899668) built a multi-body ADAMS model driven by 180 Hz, 23-marker motion capture
  plus force-plate GRF, computing **only net joint torques and resultant forces — no individual
  muscle forces or activations, and no EMG validation of any kind**. The authors' own stated
  limitation is the most important line for this task: **"How well these loads represent actual
  subject joint loads is not known."** Even this net-torque-level (not muscle-level) golf model
  has unvalidated internal loads, by the original authors' own admission.
- The one located golf-specific *musculoskeletal* (not just multibody) simulation, Bae, Cho, Kim
  & Chae 2014, "Biomechanical effect of altered lumbar lordosis on intervertebral lumbar joints
  during the golf swing: a simulation study" (*J Biomech Eng*, PMID 25162173,
  DOI 10.1115/1.4028427), used inverse dynamics on 10 professional golfers to estimate
  **intervertebral joint loads** (L5-S1 peak, decreasing toward T12) under different lumbar
  spine configurations — again joint-load level, not individual muscle force/activation level,
  and **no EMG validation is mentioned**.

**Conclusion for §7**: nobody has published a static-optimisation, CMC, or EMG-driven
muscle-activation model of the golf swing validated against golf EMG. The nearest analogues are
(a) golf-specific net-joint-torque models with explicitly unvalidated internal loads, and (b) the
generic (non-golf) validation numbers in §3/§4/§6 above, none of which were generated on a task
resembling a ~0.25 s ballistic downswing. Any activation curve this project builds for golf by
combining kinematics with a generic cost function would be a **novel, unvalidated extrapolation**,
not an application of an established, checked method.

## 8. Input requirements — is motion capture alone sufficient, or is GRF mandatory? Video-only accuracy

**GRF is not optional for a correct inverse-dynamics/static-optimisation pipeline for a dynamic
task.** Camomilla et al. 2017 (§1) states that omitting GRF/inertial terms is valid only when
inertial contribution is minor — false for anything with the segment accelerations of a golf
swing — and flags that even when GRF is measured, its own errors propagate substantially (0.01 m
centre-of-pressure error → ~14% joint-torque error). The NEM2E motion-to-EMG paper (Teramae et
al. 2025, *Front Bioeng Biotechnol*, PMID 40787196, PMC12331652, DOI 10.3389/fbioe.2025.1611414)
confirms its underlying OpenSim static-optimisation layer requires "measurements of the motions
**and ground reaction forces**" — motion alone was not sufficient for its baseline pipeline.

**Can GRF itself be estimated without a force plate, from video/motion alone?** Vonstad, Bach,
Vereijken, Su & Nilsen 2022, "Performance of machine learning models in estimation of ground
reaction forces during balance exergaming" (*J Neuroeng Rehabil*, PMID 35152877,
DOI 10.1186/s12984-022-00998-5) is the only source located that attempts this directly:
- From true 3D motion-capture kinematics, an LSTM predicted vertical GRF at **RMSE 4.3% body
  weight, R²≈0.95**.
- From plain **2D video-derived kinematics**, the same approach degraded to **RMSE 10.7% body
  weight, R²≈0.77** (a simpler XGBoost model was worse still: RMSE 19.8% BW).
- Task tested: slow, low-force **balance weight-shifting exergaming** in older adults — nothing
  resembling the impulsive, high-force, short-duration loading of a golf downswing. No claim in
  the source, and none should be inferred here, about accuracy on faster/higher-force tasks —
  error would be expected to be substantially worse, not better, extrapolating from every
  speed-related degradation pattern found elsewhere in this research (§1, §3, §6).

**Can kinematics alone (joint angles) be obtained accurately enough from video, without markers?**
Reasonably well for lower-body kinematics in the tasks tested, with clear degradation at faster
tasks and more proximal/complex joints:
- Pagnon, Domalain & Reveret 2022, "Pose2Sim: An End-to-End Workflow for 3D Markerless Sports
  Kinematics — Part 2: Accuracy" (*Sensors* 22(7):2712, PMID 35408326, PMC9002957,
  DOI 10.3390/s22072712): walking/running/cycling, single participant, vs marker-based reference.
  Coefficient of multiple correlation >0.9 (sagittal plane) for most joints, mean angle errors
  **3.0° (walking), 4.1° (running), 4.0° (cycling)** — **but hip in running collapsed to CMC=0.65
  with a systematic 15° offset**, and ankle in cycling to CMC=0.75 (partial occlusion). I.e. the
  faster task (running vs walking) produced the single worst result in the whole study, at the
  proximal joint most analogous to the hip/trunk rotation central to a golf swing.
- Yang, Sigward et al. 2025 (PMID 40425708, *Sci Rep*, PMC12117081), markerless vs marker-based
  during athlete jumping (squat/drop/countermovement jumps — the fastest, most ballistic task in
  any markerless-validation study located): sagittal-plane joint-angle RMSD **≤5.6°**, hip joint
  moment RMSD **≤0.26 N·m/kg**, joint power RMSD **≤2.12 W/kg**, knee/ankle kinematics and
  kinetics "high accuracy," but the authors explicitly single out that **"the accuracy of hip
  joint kinematic measurements in the sagittal plane requires further validation."** Kinetics
  (moments/power) in this study still depended on a force plate for GRF — markerless video
  supplied kinematics only, GRF was not derived from video.

**Conclusion for §8**: (a) GRF measurement (force plate or equivalent) is required for a valid
inverse-dynamics/optimisation pipeline on a dynamic task — no source located validates omitting
it for anything beyond slow/quasi-static movement; (b) video-only GRF *estimation* has been
demonstrated only for slow, low-force tasks, with roughly **2–2.5× worse RMSE and a ~0.18 drop in
R²** than using true 3D marker kinematics as the estimator input, even before considering a
faster task; (c) video-only *kinematics* (joint angles, no GRF) achieve single-digit-degree
accuracy in the best-documented cases, but the one study that tested a fast/ballistic task and
the one that tested running both found their **worst-case errors specifically at proximal/complex
joints under faster conditions** — precisely where a golf swing analysis would need its best
accuracy (hip and trunk rotation). No source located combines video-only kinematics with
video-only (markerless) GRF estimation and validates the resulting joint moments against ground
truth for any task, let alone a ballistic one — that full "video only, no instrumentation"
pipeline for anything beyond kinematics remains, on the evidence gathered, unvalidated.

---

## 9. Overall synthesis and status

**Is back-solving legitimate?** As a mathematically well-posed procedure with published error
bounds — yes, but only for slow, cyclic, well-characterised, near-optimal tasks (gait is the
only task with dense validation), and even there the answer is *a* plausible activation pattern
consistent with a chosen cost function or EMG constraint, never uniquely *the* activation pattern
(§2). Accuracy against real EMG ranges enormously by muscle, by task, and by whether the analysis
is group- or individual-level (§3/§4/§6 synthesis table). For a single golfer's single downswing
— an individual-level, ballistic, biarticular-muscle-heavy, proximal-joint-dominant, entirely
unvalidated-in-golf task — every documented failure mode found in this research pass (speed,
individual-level noise, biarticular muscles, proximal joints, non-optimal/idiosyncratic control)
stacks in the wrong direction simultaneously. No source located gives a number for what accuracy
to expect under that combination; extrapolating from the best-documented near-analogues (hopping,
running, walk-run transition) points toward the low end of the observed range (R²/r roughly
0.0–0.6) for at least the biarticular, proximal, and fast-recruiting muscles, not the high end.

**What EMG-informed methods buy:** for near-normal, near-optimal movement, adding measured EMG
to the standard pipeline gave only a modest ~9% RMSE reduction (§5, Princelle 2025) — but its
value rises sharply, and becomes closer to "necessary rather than nice-to-have," specifically for
movement that is idiosyncratic/individual/sub-optimal relative to a generic cost function, which
is exactly the category a single person's golf swing falls into. This is the strongest
substantive argument for constraining this project's model with the golf EMG data that does
exist (docs/research/02–04, 07) rather than relying on optimisation alone for any muscle with
measured data — and for treating any muscle with no golf EMG (F-009/F-013/F-015 family) as
having a wider, not narrower, uncertainty band when back-solved from motion alone.

**Status of this document**: all 8 numbered questions from the task brief are addressed with
cited sources above; §7 (golf-specific) is a documented negative finding (no muscle-level golf
model exists) rather than a positive result, which is itself the key finding for the project.
14 distinct sources were used (count in table below), exceeding the 12-source target. Two minor
declared gaps: no Crowninshield & Brand 1981 primary-source quantitative detail was recoverable
(abstract-only access via a citing letter, PMID 12231290); no ballistic sport-throwing-specific
(baseball pitch/javelin) static-optimisation-vs-EMG validation study was located in this pass —
flagged for a further targeted search if the project revisits this file.

---

## Running source log

| # | Source | URL/PMID | Used for |
|---|--------|----------|----------|
| 1 | Erdemir, McLean, Herzog & van den Bogert 2007, *Clin Biomech* 22(2):131-154 | PMID 17070969, doi:10.1016/j.clinbiomech.2006.09.005 | §3 framing — SO decades-old, unvalidated for clinical translation |
| 2 | Heintz & Gutierrez-Farewik 2007, *Gait Posture* 26(2):279-88 | PMID 17071088, doi:10.1016/j.gaitpost.2006.09.074 | §3 — SO vs EMG-to-force, good in plantar/dorsiflexors, worse in knee flex/ext (biarticular) |
| 3 | Rauber et al. 2024, *J Biomech* 163:111922 | PMID 38220500, doi:10.1016/j.jbiomech.2023.111922 | §3 — XCorr 0.97 (quasi-static lifting) → 0.51 (walking/running); explicit warning vs dynamic tasks |
| 4 | Michaud, Lamas, Lugrís & Cuadrado 2021, *J Neuroeng Rehabil* 18:17 | PMID 33509205, PMC7841909 | §2/§3 — 43-muscle leg model; per-muscle r 0.61–0.89, mean 0.74 (gait) |
| 5 | Princelle, Viceconti & Davico 2025, *Ann Biomed Eng* | PMID 40128488, PMC12075340 | §5 — EMG-assisted ~9% RMSE reduction; SO fails on sub-optimal/atypical control |
| 6 | Afschrift, Kistemaker, Bobbert & De Groote 2025, *PLoS Comput Biol* | PMID 41248112, PMC12622833 | §4 — predictive sim fails qualitatively at walk-run transition; cost-function overfitting risk |
| 7 | Jessup, Kelly, Cresswell & Lichtwark 2023, *R Soc Open Sci*, doi:10.1098/rsos.230393 | PMID 37885982, PMC10598413 | §4/§6 — hopping validation, R² 0.02–0.97, biarticular/flexor failure, individual-level caution |
| 8 | Bourgain, Rouch, Rouillon, Thoreux & Sauret 2022, *Sports* 10(6):91 | PMID 35736831, PMC9227529 | §7 — systematic review of 92 golf-biomechanics papers, zero muscle-modelling coverage |
| 9 | Nesbit 2005, *J Sports Sci Med*, "3D kinematic and kinetic study of the golf swing" | PMID 24627665, PMC3899667 | §7 — golf forward-dynamics model is torque-driven only; "how well these loads represent actual subject joint loads is not known" |
| 10 | Nesbit & Serrano 2005, *J Sports Sci Med*, "Work and power analysis of the golf swing" | PMID 24627666, PMC3899668 | §7 — companion golf torque/power model, no muscle-level or EMG component |
| 11 | Bae, Cho, Kim & Chae 2014, *J Biomech Eng*, doi:10.1115/1.4028427 | PMID 25162173 | §7 — golf-specific musculoskeletal inverse dynamics, joint-load (not muscle) level, no EMG validation |
| 12 | Teramae, Matsubara, Noda & Morimoto 2025 (NEM2E), *Front Bioeng Biotechnol*, doi:10.3389/fbioe.2025.1611414 | PMID 40787196, PMC12331652 | §8 — motion-to-EMG neural refinement of OpenSim SO; requires GRF; explicit warning against generalising beyond trained motions |
| 13 | Camomilla, Bergamini, Fantozzi & Vannozzi 2017, *Biomed Eng Online* 16:106 | PMID 28821242, PMC5563001 | §1 — ID error-source systematic review (67 studies); errors grow with velocity, worse for proximal joints; caution against extrapolating to high-acceleration tasks |
| 14 | Latash 2012, *Exp Brain Res* 217(1):1-5, doi:10.1007/s00221-012-3000-4 | PMID 22246105 | §2 — motor abundance reframing of Bernstein's redundancy problem; "good variance" argument against a single fixed solution |
| 15 | Thelen, Choi & Schmitz 2014, *J Biomech Eng*, doi:10.1115/1.4026358 | PMID 24390129, PMC4023657 | §4 — CMC vs in-vivo instrumented-knee contact force (4–17% peak error); biarticular EMG discrepancies |
| 16 | Vonstad, Bach, Vereijken, Su & Nilsen 2022, *J Neuroeng Rehabil*, doi:10.1186/s12984-022-00998-5 | PMID 35152877 | §8 — video-only GRF estimation, RMSE 10.7% BW / R²≈0.77 (slow task only) |
| 17 | Pagnon, Domalain & Reveret 2022 (Pose2Sim Part 2), *Sensors* 22(7):2712, doi:10.3390/s22072712 | PMID 35408326, PMC9002957 | §8 — markerless kinematics accuracy, 3–4° mean error, hip-in-running failure (CMC 0.65, 15° offset) |
| 18 | Yang et al. 2025, *Sci Rep*, athlete-jumping markerless validation | PMID 40425708, PMC12117081 | §8 — markerless kinetics in ballistic jumping, ≤5.6° angle RMSD, hip flagged as needing further validation |
| 19 | Ait-Haddou, Jinha & Herzog 2002, *J Biomech* 35(10):1433-5 (letter re: Crowninshield & Brand 1981) | PMID 12231290, doi:10.1016/s0021-9290(02)00077-5 | §2 — confirms existence/lineage of the classic SO cost-function sensitivity debate; no abstract/quantitative detail accessible in this pass |
