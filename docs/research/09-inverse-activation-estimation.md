# 09 — Inverse Methods for Estimating Muscle Activation from Observed Motion

Task: T-031 (Phase 1b, inference research). Question: can muscle activation be legitimately
back-solved from how a golf swing visually looks (motion alone, or motion + limited EMG),
and with what validated error bounds? Status: IN PROGRESS — building incrementally, one
source at a time. Sources below are cited by URL/PMID/DOI as fetched; nothing is entered
without its own citation.

---

## 1. Inverse dynamics — computing net joint moments from motion + GRF

*(sources pending)*

## 2. The muscle redundancy problem

*(sources pending)*

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

No CMC-specific (Thelen & Anderson 2006 OpenSim-style tracking controller) quantitative EMG
validation was retrieved in this pass; flagged for a further search if time allows.

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

*(sources pending)*

## 8. Input requirements — is motion capture alone sufficient, or is GRF mandatory? Video-only accuracy

*(sources pending)*

---

## Running source log

| # | Source | URL/PMID | Used for |
|---|--------|----------|----------|
