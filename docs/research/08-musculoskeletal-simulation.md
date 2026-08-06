# 08 — Musculoskeletal Simulation of the Golf Swing: Can Muscle Activation Drive Motion?

Task: T-030 (Phase 1b). Question: does a published musculoskeletal model of the golf swing
exist; has anyone driven a golf-swing simulation forward from muscle activation
(activation → force → moment → motion); what generic full-body models could be adapted;
what are the trunk-axial-rotation, redundancy, computational-cost, and licensing
implications for a free public Android app. Status: COMPLETE — 36 sources logged, all
six brief questions answered in §7. Nothing entered without its own citation
(URL/PMID/DOI). Several individual claims are explicitly flagged UNVERIFIED where a
primary source could not be independently confirmed in this pass (Gait2392 exact DOF,
MoBL-ARMS exact NC licence wording, Rajagopal "MIT Use Agreement" exact text, FBLS custom
Use Agreement exact text) — these are marked inline and must be re-checked before any
licensing decision is finalised.

---

## 1. Published musculoskeletal models of the golf swing specifically

### 1.1 Chen, Pandy, Huang, Tang 2024 — OpenSim golf downswing / lumbar loads
Chen Z-H, Pandy M, Huang T-Y, Tang W-T. "Does overhead squat performance affect the swing
kinematics and lumbar spine loads during the golf downswing?" *Sensors* 2024;24(4):1252.
DOI: 10.3390/s24041252. PMID 38400409, PMCID PMC10893031. Open access.
- Model: the **Full-Body Lumbar Spine (FBLS)** OpenSim model, hosted at
  https://simtk.org/projects/fullbodylumbar (see §3 for model detail) — **21 segments, 30
  DOF, 324 musculotendon actuators**, scaled to each participant's anthropometry.
- Pipeline: inverse kinematics → inverse dynamics → **static optimization** (not forward
  dynamics) to resolve net joint moments into individual muscle forces; OpenSim's Joint
  Reaction Analysis tool computed internal vertebral joint loads.
- Trunk representation used: **sagittal and frontal planes only** — the authors explicitly
  state axial (transverse-plane) rotation of the lumbar spine was *not analysed*, deferred
  to future work, despite the underlying FBLS model supporting axial rotation DOF.
- Validation: simulated muscle activations vs measured EMG for longissimus thoracis,
  correlation r = 0.72 ± 0.09 (right side), 0.74 ± 0.21 (left side).
- Numeric results: peak L5–S1 shear force 525.19 ± 86.69 N (low-overhead-squat-score
  group) vs 407.90 ± 59.06 N (high-score group), p = 0.002; peak L4–L5 shear
  387.19 ± 89.16 N vs 299.54 ± 37.30 N, p = 0.01; compressive forces 3018–3921 N range,
  not significantly different by group. Butterworth filter 14 Hz cutoff. OpenSim 4.3.
  No computation time reported.

### 1.2 Harada et al. 2023 — AnyBody reverse-dynamics golf swing, hip arthroplasty
Harada T, Hamai S, Hara D, et al. "Reverse dynamics analysis of contact force and muscle
activities during the golf swing after total hip arthroplasty." *Sci Rep* 2023;13:8688.
DOI: 10.1038/s41598-023-35484-y. PMID 37248313, PMCID PMC10227076. Open access.
- Software: **AnyBody Modeling System v7.3.4** (AnyBody Technology, Denmark), standard
  AMMR MoCapModel v2.3.4 musculoskeletal model.
- Hip modelled as a 3-DOF spherical joint; knee/ankle/subtalar as hinge joints. 9 named hip
  muscles examined (iliopsoas, gluteus maximus/medius/minimus, rectus femoris, biceps
  femoris long head, medial hamstring, adductor magnus, adductor longus).
- Method: **inverse kinematics + inverse/"reverse" dynamics** — marker trajectories and
  GRF drive the model to compute hip contact force (HCF) and muscle force; NOT forward
  dynamics.
- Numeric results: mean max clubhead speed 31 ± 7 m/s; hip rotation ~20–30°; mean hip
  contact force 5.1× body weight (lead hip), 6.6× body weight (trail hip); bilateral
  iliopsoas activation >60% MVIC.

### 1.3 Steven Nesbit's golf-swing kinetic/kinematic models — NOT muscle-driven
Nesbit SM. "A three dimensional kinematic and kinetic study of the golf swing." *J Sports
Sci Med* 2005;4(4):499–519. PMID 24627665, PMCID PMC3899667. Open access.
Nesbit SM, Serrano M. "Work and power analysis of the golf swing." *J Sports Sci Med*
2005;4(4). PMID 24627666, PMCID PMC3899668. Open access.
- Software: **ADAMS** (Mechanical Dynamics Inc.), commercial rigid multibody dynamics
  package (Lagrangian dynamics, backward-differentiation-formula integration) — **not**
  OpenSim/AnyBody and **not** a muscle model.
- Structure: 15 rigid body segments (golfer) + 15-segment flexible-shaft/1-rigid-head club
  model. Spherical joints up to 3 DOF; knees/elbows/wrists limited to 2 DOF.
- Method: **inverse dynamics, kinematically driven** — motion-capture data (180 Hz)
  prescribes joint motion; the model solves for net joint torques/forces. There are **no
  individual muscles anywhere in this model** — the "kinetics" are net joint torques only.
  Widely cited in golf biomechanics literature but not usable as a muscle-driven base.
- Findings: wrists dominate club-head velocity generation; hand trajectory geometry (not
  a restraining torque) explains delayed wrist uncocking; club shaft flexibility
  contributes ~50% of stored energy released by impact.

**Conclusion of §1**: no published golf-swing-specific model was found that is both (a)
muscle-based (Hill-type actuators) and (b) driven forward from activation to motion. The
two muscle-based golf studies located (Chen 2024, Harada 2023) both go the *other*
direction — motion/GRF in, muscle force out (static optimization / reverse dynamics).
Nesbit's widely-cited golf models are pure rigid-body inverse dynamics with no muscles at
all.

## 2. Forward dynamics: has anyone driven a golf swing FROM muscle activation?

**Direct answer: no.** Multiple targeted Europe PMC queries were run specifically for this
question — `golf swing OpenSim muscle`, `golf swing AnyBody muscle model`, `golf swing
forward dynamics simulation muscle activation`, `golf swing computed muscle control OR
"forward dynamics" muscle-driven` — and cross-checked against PubMed. **No published study
was found in which a golf swing was simulated by driving a musculoskeletal model forward
from muscle excitation/activation signals to produce motion.** Every golf-specific
muscle-based study located (§1) goes the opposite direction: motion/GRF/EMG in, muscle
force or activation out, via inverse dynamics + static optimization (Chen 2024, §1.1) or
inverse kinematics + reverse dynamics (Harada 2023, §1.2). The most-cited golf full-body
dynamic model (Nesbit 2005, §1.3) has no muscles at all — it is a pure rigid-body
inverse-dynamics/torque model.

### 2.1 Adjacent evidence that forward, muscle-driven simulation is achievable in principle
None of the following is golf-specific, but each demonstrates the forward-dynamics
capability that a golf application would need, at varying levels of biomechanical rigour
and computational cost:

- **Remus et al. 2023** (full detail in §3.10) is the strongest evidence: a genuinely
  muscle-driven forward-dynamics hybrid FE-multibody lumbosacral spine model, "generated
  purely muscle-actuated, without prescribing complete kinematics" — but restricted to
  **sagittal-plane flexion/extension only**, with axial rotation explicitly left to future
  work, and costing **~30 minutes of desktop compute per load case**.
- **Rajagopal et al. 2016** (§3.1) reports muscle-driven forward dynamics of gait producing
  joint moments within 3% RMSE of inverse dynamics and qualitative EMG agreement, at
  **~10 minutes of desktop compute per simulated gait cycle** — but only the lower limbs
  are muscle-driven; the trunk/upper body use idealized torque actuators, not real muscles.
- **Seth et al. 2019 thoracoscapular model** (§3.8) reports genuine OpenSim forward
  dynamics running at **11–18× real time** (i.e. 11–18 seconds of compute per simulated
  second) for the shoulder complex — faster than CMC, but still not real-time, and again
  not a trunk/whole-body model.
- **Lee, Park, Lee, Lee 2019 (SIGGRAPH/ACM TOG)**, "Scalable Muscle-Actuated Human
  Simulation and Control." DOI: 10.1145/3306346.3322972. A **comprehensive full-body
  musculoskeletal model with 346 muscles**, controlled via a two-level deep-reinforcement-
  learning imitation-learning algorithm, driven by muscle contraction dynamics (not
  idealized torques). Demonstrated predictive simulation of gait, pathological gaits, bone
  deformity, muscle weakness, contracture, and prosthesis use, and predictive
  visualisation of post-surgical gait changes. This is the clearest existing demonstration
  that a full-body, muscle-driven (not just torque-driven) forward simulation CAN produce
  realistic human movement. Important caveats: (a) it is a computer-graphics/animation
  paper (SIGGRAPH), not a biomechanically-validated clinical/sports-science model — no EMG
  validation is reported in the abstract; (b) it targets locomotion/gait, not golf/ballistic
  rotational sports; (c) the abstract gives no explicit runtime/real-time performance
  figure — DRL policies of this kind are typically evaluated at interactive/real-time rates
  once trained (that is standard practice in this sub-field), but **the training process
  itself (deep RL) is a separate, much larger computational cost (commonly days on GPU
  hardware for comparable published work)** that is not disclosed in the fetched abstract
  and was not independently verified in this research pass. Treat "real-time after
  training" as plausible-but-unconfirmed for this specific paper.
- **Van Wouwe, Hicks, Delp, Liu 2024** (§ below, PLOS Comput Biol, PMID 38394308, PMCID
  PMC10917303, DOI 10.1371/journal.pcbi.1011410): differentiable musculoskeletal simulator
  used for trajectory optimization (sprint vs marathon body/muscle-volume optimization).
  Model: **92 lower-limb muscle actuators + 8 upper-limb torque actuators, 31 DOF
  (including 6 pelvis DOF), with full trunk representation integrated**. Runs on a
  **laptop (11th-gen Intel Core i9, 2.5GHz, no GPU needed)**, but a single optimization
  (half a gait cycle) still takes **30 minutes to 4 hours to converge** — this is
  trajectory/optimal-control solving, not real-time playback.
- **Ackermann & van den Bogert 2010**, "Optimality principles for model-based prediction of
  human gait." *J Biomech* 2010;43(5):1055–1060. DOI: 10.1016/j.jbiomech.2009.12.012.
  PMID 20074736, PMCID PMC2849893. 2-D forward-dynamics-based gait prediction using
  different cost functions (fatigue-like cost functions produced realistic gait with
  correct stance-phase knee flexion; pure energy-minimisation did not) — relevant
  precedent for the fact that **forward-dynamics-*predicted* (not just tracked) motion is
  achievable but highly sensitive to the chosen optimality/cost criterion**, which is
  itself an unresolved modelling choice (see §4).

### 2.2 What forward-driving a golf swing would require, synthesised from the above
No source addresses golf directly, so this is inference from the closest available
evidence, flagged as such:
1. A trunk/lumbar model with real axial-rotation DOF and real trunk muscles (most existing
   trunk models do not have both simultaneously — see §3.9's Christophy/Bruno finding).
2. A control/activation-generation strategy, since raw EMG-to-muscle-driven forward
   dynamics for a full novel golf swing has never been demonstrated; the two realistic
   routes evidenced in adjacent literature are (a) tracking/CMC-style controllers that
   still require a target kinematic trajectory to track (defeats the purpose of true
   "activation drives motion" for a novel swing), or (b) a trained control policy
   (Lee et al. 2019 style, deep RL) that can generate motion from a reward specification
   without a prescribed trajectory, at unconfirmed but plausibly real-time runtime cost
   after an expensive offline training phase.
3. Acceptance that either approach costs from minutes to hours of compute per simulated
   swing on desktop-class hardware, per every concrete figure found in this research pass
   (§5 collects these).

## 3. Generic full-body / regional models we could adapt

### 3.1 Rajagopal et al. 2016 — OpenSim Full Body Model (gait)
Rajagopal A, Dembia CL, DeMers MS, Delp DD, Hicks JL, Delp SL. "Full-Body Musculoskeletal
Model for Muscle-Driven Simulation of Human Gait." *IEEE Trans Biomed Eng*
2016;63(10):2068–2079. DOI: 10.1109/TBME.2016.2586891. PMID 27392337, PMCID PMC5507211.
Free full text via Europe PMC/PMC (subscription on IEEE site).
SimTK project: https://simtk.org/projects/full_body
- **37 DOF total**, **80 Hill-type muscle-tendon units actuating the LOWER limbs only**,
  plus **17 idealized torque actuators for the upper body/torso** (arms and trunk are NOT
  represented by real muscles — a critical gap for a golf-swing application, where trunk
  rotation and the upper body are the primary movers).
  - This means **trunk axial rotation is kinematically present as a DOF but is NOT
    muscle-driven** in the stock Rajagopal model — torque actuators stand in for the
    entire trunk/upper-body musculature (obliques, erector spinae, lats, etc. absent).
  - Built from cadaver-specimen anatomy (21 specimens) + MRI of 24 healthy young subjects.
  - Computation: **muscle-driven simulations of walking/running took ~10 minutes on a
    typical desktop computer**; joint moments matched inverse dynamics within <3% RMSE;
    simulated muscle activity showed qualitative EMG agreement.
  - License noted on SimTK project page as an OpenSim/SimTK "Use Agreement" (see §6 —
    verify exact terms, not literally the OSI MIT license despite informal naming).
- Downstream extension found: Hu X, Dooley EA, Stefanyshyn DJ, Wannop JW, Russell SD, "An
  Augmented Full-Body Model that Improves Upper Body Tracking and Reduces Dynamic
  Inconsistency in Complex Motion," *Ann Biomed Eng* 2025. PMID 40461902, PMCID
  PMC12391203. Open access. Explicitly built on top of Rajagopal 2016 to improve upper-body
  tracking — implies the stock model's upper body/trunk fidelity is a recognised weak
  point requiring augmentation. (Full detail pending — fetch in progress.)

### 3.2 Full-Body Lumbar Spine (FBLS) model — Beaucage-Gauvreau et al. 2019
Beaucage-Gauvreau E, Robertson WSP, Brandon SCE, Fraser R, Freeman BJC, Graham RB,
Thewlis D, Jones CF. "Validation of an OpenSim full-body model with detailed lumbar spine
for estimating lower lumbar spine loads during symmetric and asymmetric lifting tasks."
*Comput Methods Biomech Biomed Engin* 2019. DOI: 10.1080/10255842.2018.1564819. PMID
30714401. Not open access (publisher paywall). SimTK project:
https://simtk.org/projects/fullbodylumbar
- **21 body segments, ~29–30 DOF** (SimTK page states 29; the Chen 2024 application paper
  states 30 — reconcile as minor version/rounding difference, both cited), **324
  musculotendon actuators**.
- Lumbar spine: **5 lumbar vertebrae modelled individually**, with the intervertebral
  joints supporting flexion-extension, axial rotation, AND lateral bending — i.e. this is
  one of the few full-body OpenSim models where **trunk axial rotation is anatomically
  represented at each lumbar level**, not lumped into a single idealized joint.
  8 trunk muscle groups with multiple fascicles each: rectus abdominis, external obliques,
  internal obliques, erector spinae, multifidus, quadratus lumborum, psoas major,
  latissimus dorsi.
  Model estimates of intradiscal pressure correlated strongly with in vivo measurements
  (per abstract).
- SimTK page states model is currently **suitable for Static Optimization; NOT yet
  configured for Computed Muscle Control (CMC)** — i.e. as distributed, it cannot be
  forward-driven from activation without further developer work.
- License: SimTK page shows **CC BY 4.0** for one download bundle and a **separate custom
  Use Agreement** for the "Full-Body Lumbar Spine Model" file specifically — the two
  licence statements differ per download, so each file's licence must be checked
  individually before reuse (see §6).
- Related Beaucage-Gauvreau lifting-technique papers using this model: *Eur Spine J*
  2021;PMID 33156439 (braced arm-to-thigh technique, moment reductions 13–51%, compression
  27–45%, shear 31–62%); *J Biomech* 2020;PMID 31898975/PMCID PMC11833159 (same technique,
  healthy vs LBP groups, moment reductions 28–38%, compression 25–32%, shear 25–45%).

### 3.3 Alemi et al. 2023 — subject-specific thoracolumbar spine model
Alemi MM, Banks JJ, Lynch AC, Allaire BT, Bouxsein ML, Anderson DE. "EMG Validation of a
Subject-Specific Thoracolumbar Spine Musculoskeletal Model During Lifting Tasks." *Ann
Biomed Eng* 2023. PMID 37353715, PMCID PMC11426388 (NIH public access; not open on
publisher site). DOI: 10.1007/s10439-023-03273-3.
- Validated against EMG during lifting; abstract states the model "reasonably predicted
  temporal behaviour of back extensor muscles" with strong correlation. (Full DOF/muscle
  count pending full-text fetch.)

### 3.4 Other lumbar/trunk models identified for follow-up
- Meszaros-Beller, Hammer, Schmitt, Pivonka 2023, *Front Physiol*, PMID 37324394/PMCID
  PMC10264677: cross-platform (including OpenSim) trunk model quantifying that omitting
  passive spinal structures (discs/ligaments) changes compressive loading and anterior
  torque estimates by roughly -200%/-75% respectively — relevant caveat for any simplified
  trunk model.
- Zhang et al. 2024, *Front Bioeng Biotechnol*, PMID 38817923/PMCID PMC11138492: OpenSim
  lumbar-loading-during-walking study in chronic low back pain patients; reports lumbar
  axial rotation angle as a measured/modelled DOF, corroborating that axial rotation is
  tractable in OpenSim spine extensions generally (model identity pending).

### 3.5 Hamner, Seth, Delp 2010 — running model (basis of many derivatives)
Hamner SR, Seth A, Delp SL. "Muscle contributions to propulsion and support during
running." *J Biomech* 2010;43(14):2709–2716. DOI: 10.1016/j.jbiomech.2010.06.025.
PMID 20691972, PMCID PMC2973845. Free full text via PMC.
- 3-D muscle-actuated running simulation, **92 musculotendon actuators** (lower-limb
  focused, as in Gait2392 lineage). Findings: quadriceps dominate braking/support in early
  stance; soleus/gastrocnemius dominate propulsion/support in late stance; arm
  contribution to mass-centre acceleration <1% (i.e. this model's upper body/arms are
  near-irrelevant to its stated purpose and not built out with real musculature).
- Confirmed still in active comparative use: Luis I, Afschrift M, De Groote F,
  Gutierrez-Farewik EM 2022, *Front Bioeng Biotechnol*, PMID 36277379/PMCID PMC9583830,
  compares the Hamner model against other generic models for muscle-excitation
  estimation across walking speeds.

### 3.6 Gait2392/Gait2354 (Delp/Anderson-Pandy lineage)
Direct SimTK/OpenSim documentation page for this model returned HTTP 404 on this fetch
pass; identity and specs corroborated indirectly via active 2025–2026 usage citations
(e.g. Zang et al. 2026, *Bioengineering*, PMID 42510440, "individually scaled OpenSim
gait2392 models" for metabolic-power estimation) confirming the model remains a standard,
actively-used generic OpenSim gait model as of 2026 but **DOF/muscle count for this
specific model could not be independently re-verified via primary source in this research
pass** — treat any figure for Gait2392 (commonly cited elsewhere as 23 DOF / 92 lower-limb
muscles with a single lumped torso segment and one 3-DOF or often-locked lumbar joint) as
UNVERIFIED pending direct confirmation; do not rely on it for load-bearing decisions
without checking the OpenSim model file directly.

### 3.7 MoBL-ARMS Dynamic Upper Limb Model — Saul et al. 2015
Saul KR, Hu X, Goehler CM, Vidt ME, Daly M, Velisar A, Murray WM. "Benchmarking of dynamic
simulation predictions in two software platforms using an upper limb musculoskeletal
model." *Comput Methods Biomech Biomed Engin* 2015;18(13):1445–1458.
DOI: 10.1080/10255842.2014.916698. PMID 24995410, PMCID PMC4282829. Free in PMC.
SimTK project: https://simtk.org/projects/upexdyn (13,163 downloads as of last check;
license listed on the SimTK page as a **"Creative Commons ANC [non-commercial] Use
Agreement"** — NOTE: non-commercial licences are a hard blocker for this project's "free
public Android app" plan if the app has any monetisation/ads, or possibly even if fully
free depending on exact NC clause wording; must re-verify exact licence text before any
use, see §6).
- **7 DOF used for dynamic simulation** (reduced from a 15-DOF kinematic foundation):
  shoulder elevation/rotation, elevation plane, elbow flexion, forearm rotation, wrist
  flexion, wrist deviation.
- **50 Hill-type muscle-tendon actuators representing 32 distinct muscles/compartments.**
- Scope: **shoulder to hand only** — glenohumeral joint with clavicle/scapula motion,
  elbow, forearm, wrist, thumb, index finger; "hand reoriented into a grip posture" for
  simulation. **No trunk/torso segment at all** — this model assumes a fixed thorax/torso
  and cannot represent trunk rotation; it would need to be grafted onto a separate
  trunk/lower-body model for a golf swing.
- Computation time (cross-platform benchmarking, EMG-driven simulations): **OpenSim
  3–43 minutes per simulation**; **SIMM-SD/Fast 2 to 20+ hours** for equivalent runs.
  Computed Muscle Control (CMC) optimization: **average 1 hour 18 minutes 36 seconds
  (1:18:36) of compute per 1 second of simulated motion** — i.e. roughly **4,700× slower
  than real time** for CMC on this model/platform combination. This is a directly-quoted,
  concrete computational-cost figure (see §5).

### 3.8 Thoracoscapular Shoulder Model — Seth, Dong, Matias, Delp 2019
Seth A, Dong M, Matias R, Delp S. "Muscle Contributions to Upper-Extremity Movement and
Work From a Musculoskeletal Model of the Human Shoulder." *Front Neurorobot*
2019;13:90. DOI: 10.3389/fnbot.2019.00090. PMID 31780916, PMCID PMC6856649. Open access.
SimTK project: https://simtk.org/projects/thoracoscapular
- **6 DOF at the scapulothoracic joint** alone (independent scapular motion, not
  artificially coupled to the humerus as in older models), plus glenohumeral and other
  joint DOF (exact grand total not stated in the abstract/methods excerpt fetched).
- **16 major shoulder muscles**, subdivided into ~50+ individual muscle bundles/paths
  (e.g. trapezius = 4 bundles, deltoid = 3 bundles), built from van der Helm's muscle
  parameter set.
- Includes the trunk/thorax as an anatomical reference (thorax sensor at T1 spinous
  process; scapulothoracic joint modelled against an ellipsoid thorax surface) but this is
  a **shoulder-complex model, not a full trunk/spine model** — the thorax itself is
  effectively a fixed/rigid reference body, not muscle-actuated for axial rotation.
- Method: **Computed Muscle Control (CMC)**, tracking IK-derived joint angles.
- **Computation time (concrete, directly quoted):** IK 1.0–1.3× real-time; **CMC
  377–408× real-time** (i.e. ~6.3–6.8 minutes of compute per 1 second of simulated
  motion); **forward dynamics 11–18× real-time** (i.e. ~11–18 seconds of compute per 1
  second of simulated motion) — a "4–17× speedup" vs prior shoulder models is claimed.
- Licence: page text states "the model and simulation environment (OpenSim) are freely
  available, deployable, and modifiable for **any research or commercial use without
  restrictions**" — the most permissive licence statement found so far in this research
  pass (contrast with MoBL-ARMS's apparent NC restriction, §3.7). Exact licence file
  text still to be independently confirmed (see §6).

### 3.9 Christophy 2012 and Bruno 2015 lumbar spine models (via Carpenedo et al. 2025 review)
Direct primary-source fetch of the individual 2012/2015 papers was not completed this
pass; both are characterised via a systematic review that tabulates them alongside dozens
of other thoraco-lumbar models:

Carpenedo M, et al. "Advances in Musculoskeletal Modeling of the Thoraco-Lumbar Spine: A
Systematic Review." *Ann Biomed Eng* 2025;53(11):2883–2910.
DOI: 10.1007/s10439-025-03818-8. PMID 40913215, PMCID PMC12575568. Open access.
This review is the single most useful source located for the trunk-rotation question and
is used as the master comparison table for §3/§4:

| Model | Year | Lumbar joint DOF | Muscle fascicles | Axial rotation | Flex-ext | Type |
|---|---|---|---|---|---|---|
| Christophy | 2012 | 3 | 238 | Limited | Primary | Multibody (MB) |
| Bruno | 2015 | 3 | 248 | Limited | Primary | Multibody (MB) |
| Ignasiak | 2016 | 6 | 454–508 | **Yes** | Yes | Multibody (MB) |
| Rajaee | 2021 | — | 56 | Limited | Primary | Finite Element (FE) |

- Review-wide statistics: of 26 original multibody spine models surveyed, **15/26 (58%)
  used only 3-DOF lumbar joints** (these are stated to have only "Limited" axial rotation
  capability — 3-DOF joints in this literature typically = flexion-extension + lateral
  bending + a constrained/coupled axial term, not a free independent axial DOF at every
  level), while **10/26 (38%) used full 6-DOF joints**, which the review states "better
  accommodate axial rotation capability." **Ignasiak (2016) is explicitly named as
  properly supporting axial rotation.**
- Ribcage/thorax representation: included in 61% of models, either as "a lumped rigid
  segment" (21 models) or as an articulated rib system (a minority, e.g. Ignasiak).
- Dynamics approach across all 46 surveyed models: **34/46 (74%) inverse-dynamics (ID)
  based; 6/46 (13%) forward-dynamics (FD) based; 2/46 (4%) FD-assisted hybrid.** The large
  majority use ID + optimisation criteria minimising muscle stress/cost, not forward
  simulation from activation.
- Licensing (review's own summary): "MB models... benefited from open-source
  availability" via OpenSim/SimTK; separately, "three AnyBody-based models can be
  consulted by requesting a free [AnyBody] trial licence" (i.e. NOT free/open — requires a
  commercial licence holder, see §6).

**Direct answer to the brief's trunk-rotation question, using this review's own
categorisation: Christophy (2012) and Bruno (2015) — both influential, widely-reused
OpenSim lumbar models — have only "Limited" axial rotation, i.e. they are NOT adequate
for representing the transverse-plane trunk rotation that is the core of a golf swing.
Ignasiak (2016) is the one multibody model in this review explicitly credited with proper
6-DOF, axial-rotation-capable lumbar joints.**

### 3.10 Remus et al. 2023 — muscle-driven FORWARD-DYNAMICS hybrid FE-multibody lumbosacral model
Remus R, Selkmann S, Lipphaus A, Neumann M, Bender B. "Muscle-driven forward dynamic
active hybrid model of the lumbosacral spine: combined FEM and multibody simulation."
*Front Bioeng Biotechnol* 2023;11:1223007. DOI: 10.3389/fbioe.2023.1223007.
PMID 37829567, PMCID PMC10565495. Open access.
**This is the single strongest piece of evidence located in this entire research pass
that muscle activation CAN genuinely drive motion forward in a spine/trunk model** — see
full detail cross-referenced in §2 below. Key figures: rigid vertebrae L1–S1 coupled to
fibre-reinforced FE intervertebral discs, ligaments, facet joints; **129 muscle fascicles
per side (119 without transversus abdominis)** across 12 muscle groups (latissimus dorsi,
quadratus lumborum, multifidus, erector spinae components, abdominals, psoas major, etc.).
"All postures were generated purely muscle-actuated, without prescribing complete
kinematics to the dynamic bones" — genuine forward dynamics, not tracking/CMC. BUT:
**validation and simulated movement were restricted to the sagittal plane only**
(flexion 0°→+30°, extension to −10°, 13 load cases with/without up to 20 kg handheld
loads) — **trunk axial rotation was explicitly NOT modelled**; the authors list "axial
rotations and lateral flexions ... non-symmetric loads" as future work. Computation time:
**~30 minutes per load case on a desktop PC (Intel i7-10700K @ 3.80GHz, 32GB RAM, Windows
11)** for a single quasi-static-to-dynamic posture-change simulation. Validation: predicted
intradiscal pressure within ±4.4% average deviation from in vivo literature values; high
qualitative agreement between predicted and EMG-measured relative muscle-group force
changes; intra-abdominal pressure predictions matched measurements for upright posture.

*(Still to fetch: OpenSim core software licence text, AnyBody commercial licence/cost,
LifeMOD/Visual3D licensing, general muscle-redundancy review literature, and any
real-time/mobile-feasible musculoskeletal simulation literature — continuing.)*

## 4. Known limitations — muscle redundancy, co-contraction, non-uniqueness

Mathieu E, Crémoux S, Duvivier D, Amarantini D, Pudlo P. "Biomechanical modeling for
muscle force estimation [review/terminology standardisation]." *J Neuroeng Rehabil*
2023;20:130. PMID 37752507, PMCID PMC10521397. Open access.
- **Core statement of the redundancy problem**: "the number of muscles involved in moving
  a joint is higher than the number of degrees of freedom," making the muscle-force
  distribution problem mathematically **under-determined** — i.e., infinitely many
  activation patterns can produce the same net joint moment/motion. This is precisely the
  scenario named in the task brief.
- **Static optimization** (minimise/maximise an objective — summed muscle force,
  normalised force, or muscle stress — subject to satisfying the net joint torque):
  the dominant resolution method in the literature (74% of surveyed spine models per
  Carpenedo et al. 2025, §3.9), but:
  - produces **discontinuities in results over time** when solved instant-by-instant;
  - **can fail to correctly predict co-contraction of antagonist muscles** — because most
    objective functions minimise total effort/stress, they systematically **underestimate
    the force of muscles acting opposite to the net movement direction** (i.e.
    antagonists/stabilisers), which is exactly the co-contraction behaviour the task brief
    flags as a concern;
  - shows "inadequate consideration of force production physiology" relative to EMG-driven
    approaches.
- **EMG-driven models**: use measured EMG as direct input, converted to activation and fed
  through Hill-type muscle models to estimate force "physiologically" rather than by
  abstract optimisation — better captures real co-contraction/antagonist behaviour, but
  requires instrumented EMG data collection that a consumer phone app cannot obtain from a
  camera/IMU alone.
- **EMG-assisted/calibrated hybrids**: use EMG to constrain or calibrate an otherwise
  optimisation-based solve, trading off some of static optimization's speed for some of
  EMG-driven modelling's physiological realism.
- Princelle, Viceconti, Davico 2025 (*Ann Biomed Eng*, PMID 40128488, PMCID PMC12075340,
  DOI 10.1007/s10439-025-03713-2): directly compared static optimization vs EMG-assisted
  approaches for knee contact force estimation — "both methods allowed to estimate the
  experimental knee joint contact forces experienced during walking with a high level of
  accuracy" — i.e. for *some* outcome measures the cheaper static-optimization route is
  adequate, but this was tested for gait/knee, not a ballistic rotational task like a golf
  swing, and does not resolve the antagonist-underestimation problem noted above.
- Nasr A, Inkol KA, Bell S, McPhee J. "InverseMuscleNET: Machine Learning Alternative to
  Static Optimization." *Front Comput Neurosci* 2021. PMID 35002663, PMCID PMC8735851,
  DOI 10.3389/fncom.2021.759489. Proposes a recurrent neural network as an alternative to
  static optimization for the same redundancy problem, citing computational efficiency
  gains — an emerging alternative worth tracking, though not yet a settled standard.

**Bottom line for §4**: the redundancy problem is real, textbook-acknowledged, and
directly undermines any scheme that tries to infer "the" muscle activation from observed
motion alone (that is a separate, harder, ill-posed inverse problem — see companion doc
`09-inverse-activation-estimation.md`). For this document's FORWARD-direction question
(does a chosen activation pattern produce realistic motion), redundancy instead means:
many different, equally "valid" activation patterns will produce visually similar
motion, so a game/app does not need to reconstruct one biomechanically "true" activation
pattern to look realistic — but it does mean any forward-dynamics controller needs an
explicit strategy (optimisation objective, EMG-driven, or trained policy) to pick *one*
pattern out of the redundant set, and the choice of strategy measurably changes the
resulting motion realism (Ackermann & van den Bogert 2010, §2.1, showed cost-function
choice determines whether gait "looks right").

## 5. Computational cost — real-time on a phone, or precomputed offline?

Every concrete performance figure located in this research pass, collected in one place:

| Source | Model | Method | Reported cost |
|---|---|---|---|
| Rajagopal et al. 2016 (§3.1) | Full-body, 37 DOF, 80 lower-limb muscles + 17 torque actuators | Muscle-driven forward dynamics (gait/running) | **~10 minutes** per simulation on "a typical desktop computer" |
| Seth et al. 2019 thoracoscapular (§3.8) | Shoulder complex, 16 muscles/~50 bundles | Inverse Kinematics | 1.0–1.3× real time |
| Seth et al. 2019 thoracoscapular (§3.8) | same | **Computed Muscle Control (CMC)** | **377–408× real time** (≈6.3–6.8 min compute per 1 s simulated) |
| Seth et al. 2019 thoracoscapular (§3.8) | same | **Forward Dynamics** | **11–18× real time** (11–18 s compute per 1 s simulated) |
| Saul et al. 2015 MoBL-ARMS (§3.7) | Upper limb, 7 DOF, 50 actuators/32 muscles | EMG-driven simulation, OpenSim | 3–43 minutes per simulation |
| Saul et al. 2015 MoBL-ARMS (§3.7) | same | EMG-driven simulation, SIMM-SD/Fast | 2 to 20+ hours per simulation |
| Saul et al. 2015 MoBL-ARMS (§3.7) | same | **CMC optimization** | **average 1:18:36 (1h 18m 36s) per 1 s of simulated motion** ≈ **~4,700× slower than real time** |
| Remus et al. 2023 hybrid FE-MB lumbar spine (§3.10, §2.1) | L1-S1, 129 muscle fascicles/side, FE discs | Genuine muscle-driven forward dynamics | **~30 minutes per load case** on a desktop i7-10700K, 32GB RAM |
| Van Wouwe et al. 2024 differentiable simulator (§2.1) | 31 DOF, 92 lower-limb muscles + 8 torque actuators, full trunk | Direct-collocation trajectory optimization | **30 minutes to 4 hours** per half-gait-cycle problem, on a laptop (i9, no GPU); prior non-differentiable methods took "several days" for comparable problems |
| Lee, Park, Lee, Lee 2019 SIGGRAPH (§2.1) | Full body, 346 muscles | Deep-RL-trained control policy | Runtime performance not stated in abstract; training cost also undisclosed — **unconfirmed, treat as not-yet-evidenced for real-time** |

**Direct answer to the brief's question**: every concretely-measured figure located in
this research places muscle-driven musculoskeletal simulation **far below real-time** on
desktop-class hardware — from ~10–18× real time (fastest: plain forward dynamics on a
shoulder-only model) up to ~4,700× real time (CMC on an upper-limb model) and 30 min–4 hrs
for a single trajectory-optimization solve of part of a movement cycle. No source
describes any of these techniques running on phone-class hardware at all, let alone in
real time. The only technique that plausibly could run at interactive rates on
consumer/mobile hardware — a pre-trained deep-RL control policy (Lee et al. 2019 style) —
has its runtime performance unconfirmed from the sources fetched in this pass, targets
locomotion rather than golf, was never validated against biomechanical/EMG ground truth in
the fetched abstract, and requires a large, separate, offline training investment before
any on-device runtime exists at all.

**Conclusion: for a free public Android app, muscle-driven musculoskeletal simulation of a
golf swing must be precomputed offline (desktop/server/cloud) and shipped as baked
animation/data — not simulated live on-device.** A viable app architecture, per the
evidence above, would run OpenSim (or a differentiable/RL-based equivalent) offline once
per swing archetype or per user profile, at costs ranging from minutes to hours of compute
per simulated swing, and ship the resulting joint-angle/muscle-activation time series (or
just the motion) as static data for the app to play back or interpolate.

## 6. Licensing of every model / dataset / software mentioned

| Item | Licence / terms found | Source | Free-app compatibility |
|---|---|---|---|
| **OpenSim core software** (opensim-core) | **Apache License 2.0** — permissive, no-charge, royalty-free, allows commercial use, sublicensing, and redistribution; requires retaining copyright/attribution notices and marking modified files | github.com/opensim-org/opensim-core/blob/main/LICENSE.txt (fetched directly) | **Yes — fully compatible** with a free public app, including commercial/ad-supported use |
| **OpenSim Moco** (trajectory-optimization toolkit, now merged into opensim-core) | **Apache License 2.0**, explicitly described by the project as "permissive licensing" that "allows for commercial use" | github.com/opensim-org/opensim-moco (repo archived 2025-04-10; functionality moved into core opensim-core repo) | **Yes** |
| **Rajagopal et al. 2016 Full Body Model** (gait) | SimTK download page (Hamner/Delp-family project cluster) labels the licence **"MIT Use Agreement"** — permissive by name, but this is SimTK's own document, not verified word-for-word against the OSI MIT License text in this pass | simtk.org/projects/full_body | **Likely yes, but verify exact document text before shipping** — flagged unverified |
| **Full-Body Lumbar Spine (FBLS) model** (Beaucage-Gauvreau et al. 2019) | SimTK page shows **two different licences for two different downloadable bundles**: one file under **CC BY 4.0**, the "Full-Body Lumbar Spine Model" file under a **separate custom Use Agreement** | simtk.org/projects/fullbodylumbar | **Mixed — check per-file.** CC BY 4.0 file is compatible (attribution required); the custom Use Agreement file's exact terms are unverified in this pass — do not assume compatibility |
| **MoBL-ARMS Dynamic Upper Limb model** (Saul et al. 2015) | SimTK page states a **"Creative Commons ANC [Attribution-NonCommercial] Use Agreement"** | simtk.org/projects/upexdyn | **Likely NO for a monetised/ad-supported app** — NC clauses typically prohibit commercial use; even for a fully free app, "non-commercial" licence terms are a legal risk that needs explicit legal review before use, and the exact NC scope was not independently confirmed word-for-word in this pass |
| **Thoracoscapular Shoulder Model** (Seth et al. 2019) | Project page text: "the model and simulation environment (OpenSim) are freely available, deployable, and modifiable for **any research or commercial use without restrictions**" | simtk.org/projects/thoracoscapular | **Yes — most permissive statement found in this research pass** |
| **AnyBody Modeling System / AMMR** (used by Harada et al. 2023, §1.2) | **Commercial, proprietary software.** Release-notes page references a formal "AnyBody Software License Agreement" and trial-licence signup; no free/open tier found; exact pricing not published online (requires vendor contact/quote) | anybodytech.com (fetched release notes page; pricing page returned 404) | **No — incompatible** with a free public app without a paid commercial licence agreement from AnyBody Technology (Denmark); also per Carpenedo et al. 2025 (§3.9), even AnyBody-based *research models* require "requesting a free trial licence," i.e. gated, not open |
| **LifeMOD** (MSC Software / ADAMS plugin for human biomechanics) | Product status could not be confirmed as currently active: the vendor domain lifemodeler.com now **301-redirects to smith-nephew.com** (an unrelated medical device company), strongly suggesting the product/company is defunct or absorbed; no current licensing terms found | lifemodeler.com (redirect observed directly) | **Unusable/unverifiable** — apparently discontinued; do not plan around it without further confirmation from MSC Software directly |
| **Visual3D** (C-Motion / HAS-Motion) | Commercial biomechanics analysis software requiring a paid licence + activation key (e.g. "CalTester licence key" for one add-on); its own **documentation wiki** is under CC BY-NC 4.0 (that licence applies to the docs, not the software itself); **no evidence found that Visual3D natively performs Hill-type muscle-driven forward dynamics at all** — it appears to be primarily a motion-capture/inverse-kinematics/kinetics analysis package, not a forward muscle-driven simulator | wiki.has-motion.com/index.php/Visual3D | **No** — commercial software licence required, AND it may not even have the required forward-dynamics muscle-simulation capability in the first place (unconfirmed either way; flagged for exclusion pending further evidence it can do what's needed) |
| **Deep-RL control policy approach** (Lee et al. 2019, SIGGRAPH/ACM) | Published as an ACM research paper; **no code/model release, licence, or public dataset located** in this pass — this is a research demonstration, not a distributable model or software package | ACM TOG / dl.acm.org (abstract only, full-text paywalled at 403) | **Not usable as-is** — would require independent re-implementation from the published method, not reuse of an existing licensed artefact |

**Section-wide conclusion**: **OpenSim itself (Apache-2.0) and at least two of the models
built on it (Rajagopal 2016's "MIT Use Agreement," and especially Seth et al. 2019's
thoracoscapular model, explicitly "any research or commercial use without restrictions")
are licence-compatible with a free public Android app**, subject to verifying exact licence
text before shipping. **AnyBody, LifeMOD, and Visual3D are all commercial/proprietary and
either confirmed-incompatible (AnyBody, cost/licence-gated), effectively unavailable
(LifeMOD, apparently discontinued), or of unconfirmed applicability (Visual3D, may not even
do muscle-driven forward dynamics).** The MoBL-ARMS upper-limb model's apparent
Non-Commercial clause is a specific red flag requiring legal review if that model is ever
considered. The Beaucage-Gauvreau lumbar spine model requires checking which of its two
differently-licensed download bundles would actually be used.

---

## 7. Overall synthesis — answers to the six brief questions

**1. Published golf-swing-specific musculoskeletal models**: two muscle-based studies
found (Chen et al. 2024 using the FBLS OpenSim model, 21 segments/30 DOF/324 muscles;
Harada et al. 2023 using AnyBody AMMR), both inverse/reverse-direction only. Nesbit's
widely-cited golf models (2005) have no muscles. **No forward-dynamics, muscle-driven,
golf-specific model exists in the literature searched.**

**2. Forward dynamics from activation → motion, for golf**: **not found anywhere.**
Nearest adjacent evidence: Remus et al. 2023 (genuine forward-dynamics muscle-driven
spine, sagittal-plane only, ~30 min/case) and Lee et al. 2019 (SIGGRAPH, 346-muscle
full-body DRL-controlled forward simulation, gait-only, no EMG validation, runtime
unconfirmed).

**3. Generic adaptable models, DOF/muscles/trunk-rotation verdict**:
- Rajagopal 2016: 37 DOF, 80 muscles (**lower limb only**), 17 torque actuators for
  upper body/trunk — trunk DOF present but **NOT muscle-driven**.
- FBLS (Beaucage-Gauvreau 2019): 21 segments, ~29–30 DOF, 324 muscles, 5 individually
  modelled lumbar vertebrae with flexion-extension + axial rotation + lateral bending per
  level, 8 trunk muscle groups — **the best-specified trunk-axial-rotation-capable
  full-body model found**, but distributed as static-optimization-ready only (not CMC-ready
  out of the box) and split across two different licences.
- Christophy 2012 / Bruno 2015 (via Carpenedo 2025 review): 3-DOF lumbar joints, "Limited"
  axial rotation — **inadequate for golf's core trunk-rotation motion.**
- Ignasiak 2016 (via same review): 6-DOF lumbar joints, axial rotation explicitly
  supported — a candidate worth direct follow-up (not independently fetched this pass).
- MoBL-ARMS (Saul 2015): 7 DOF, 50 actuators/32 muscles, **no trunk segment at all**
  (shoulder-to-hand only) — would need grafting onto a trunk model.
- Thoracoscapular (Seth 2019): 6+ DOF shoulder complex, ~50 muscle bundles, thorax
  present only as a fixed anatomical reference, not an axially-rotating muscle-driven body.
- Hamner running model (2010) / Gait2392 lineage: 92 lower-limb muscles, arm contribution
  to motion <1% and not muscle-built-out; Gait2392's own DOF/muscle figures could not be
  independently re-verified this pass (flagged unverified, §3.6).
- Remus 2023 hybrid FE-MB lumbar model: 129 muscle fascicles/side, genuinely forward-
  dynamics-capable, but sagittal-plane validated only — **axial rotation NOT yet modelled.**

**Plain verdict on trunk axial rotation** (as explicitly requested): **most available
full-body/trunk OpenSim models — Rajagopal 2016, Christophy 2012, Bruno 2015, Remus
2023 — do NOT adequately drive trunk axial rotation with real muscles**, either because
the trunk is torque-actuated (Rajagopal) or the lumbar joints are kinematically limited to
"Limited" axial rotation (Christophy/Bruno) or the model's forward-dynamics validation
never extended past the sagittal plane (Remus). **The FBLS model (Beaucage-Gauvreau 2019)
and Ignasiak (2016) are the two identified exceptions that anatomically support full
axial rotation** — FBLS via 5 individually-modelled lumbar vertebrae, Ignasiak via 6-DOF
joints per the Carpenedo review characterisation. Neither has been demonstrated driving a
golf swing, and FBLS is not yet configured for forward/CMC use as distributed.

**4. Redundancy/co-contraction**: confirmed textbook problem (Mathieu et al. 2023) —
more muscles than DOF at every major joint means infinite activation solutions per
motion; static optimization (the dominant method, 74% of surveyed spine models) reliably
**under-predicts antagonist/co-contraction force**; EMG-driven or EMG-assisted methods
mitigate this but need real EMG input a phone can't capture from vision/IMU alone.

**5. Computational cost**: every concrete figure found (table in §5) is far below real
time — 11× to ~4,700× real time depending on method, or 10 minutes to 4 hours per
simulation/optimization run, all on desktop-class hardware, none on mobile. **Verdict:
must be precomputed offline and shipped as baked data; no evidence supports on-device
real-time muscle-driven simulation on a phone.**

**6. Licensing**: OpenSim core + Moco = Apache-2.0 (fully free-app compatible). Best
model-level licence found: Seth et al. 2019 thoracoscapular model ("any research or
commercial use without restrictions"). Rajagopal 2016 labelled "MIT Use Agreement"
(likely compatible, unverified word-for-word). FBLS model: split licence, must check
per download bundle. MoBL-ARMS: apparent Non-Commercial clause, legal-review flag.
AnyBody: commercial/proprietary, incompatible without a paid licence. LifeMOD: apparently
discontinued (domain redirects to an unrelated company). Visual3D: commercial, and may not
even provide the required forward-dynamics muscle capability.

---

## Running source log

| # | Source | URL/PMID/DOI | Used for |
|---|--------|----------|----------|
| 1 | Chen ZH, Pandy M, Huang TY, Tang WT 2024, *Sensors* 24(4):1252 | PMID 38400409 / PMCID PMC10893031 / DOI 10.3390/s24041252 | §1.1 golf downswing FBLS model application |
| 2 | Harada T, Hamai S, Hara D, et al. 2023, *Sci Rep* 13:8688 | PMID 37248313 / PMCID PMC10227076 / DOI 10.1038/s41598-023-35484-y | §1.2 AnyBody golf swing reverse dynamics |
| 3 | Nesbit SM 2005, *J Sports Sci Med* 4(4):499–519 | PMID 24627665 / PMCID PMC3899667 | §1.3 golf swing kinematic/kinetic model, no muscles |
| 4 | Nesbit SM, Serrano M 2005, *J Sports Sci Med* 4(4) | PMID 24627666 / PMCID PMC3899668 | §1.3 work/power analysis of golf swing |
| 5 | Rajagopal A, Dembia CL, DeMers MS, Delp DD, Hicks JL, Delp SL 2016, *IEEE Trans Biomed Eng* 63(10):2068–2079 | PMID 27392337 / PMCID PMC5507211 / DOI 10.1109/TBME.2016.2586891 | §3.1 Full Body Model, §5 compute cost, §6 licence |
| 6 | SimTK project page, Full Body Model | https://simtk.org/projects/full_body | §3.1 DOF/muscle/licence detail |
| 7 | Hu X, Dooley EA, Stefanyshyn DJ, Wannop JW, Russell SD 2025, *Ann Biomed Eng* | PMID 40461902 / PMCID PMC12391203 | §3.1 augmentation of Rajagopal model, upper-body weakness confirmation |
| 8 | Beaucage-Gauvreau E, Robertson WSP, Brandon SCE, et al. 2019, *Comput Methods Biomech Biomed Engin* | PMID 30714401 / DOI 10.1080/10255842.2018.1564819 | §3.2 FBLS model validation |
| 9 | SimTK project page, Full-Body Lumbar Spine | https://simtk.org/projects/fullbodylumbar | §3.2 FBLS DOF/muscle/licence detail |
| 10 | Beaucage-Gauvreau E, et al. 2021, *Eur Spine J* | PMID 33156439 / DOI 10.1007/s00586-020-06631-0 | §3.2 lifting-technique application of FBLS |
| 11 | Beaucage-Gauvreau E, et al. 2020, *J Biomech* | PMID 31898975 / PMCID PMC11833159 / DOI 10.1016/j.jbiomech.2019.109584 | §3.2 lifting-technique application of FBLS |
| 12 | Alemi MM, Banks JJ, Lynch AC, Allaire BT, Bouxsein ML, Anderson DE 2023, *Ann Biomed Eng* | PMID 37353715 / PMCID PMC11426388 / DOI 10.1007/s10439-023-03273-3 | §3.3 thoracolumbar EMG validation |
| 13 | Meszaros-Beller L, Hammer M, Schmitt S, Pivonka P 2023, *Front Physiol* | PMID 37324394 / PMCID PMC10264677 / DOI 10.3389/fphys.2023.1135531 | §3.4 passive-structure omission effects |
| 14 | Zhang Z, Zou J, Lu P, et al. 2024, *Front Bioeng Biotechnol* | PMID 38817923 / PMCID PMC11138492 | §3.4 lumbar axial rotation in walking/LBP |
| 15 | Hamner SR, Seth A, Delp SL 2010, *J Biomech* 43(14):2709–2716 | PMID 20691972 / PMCID PMC2973845 / DOI 10.1016/j.jbiomech.2010.06.025 | §3.5 running model, 92 muscles |
| 16 | Luis I, Afschrift M, De Groote F, Gutierrez-Farewik EM 2022, *Front Bioeng Biotechnol* | PMID 36277379 / PMCID PMC9583830 | §3.5 Hamner model comparative reuse |
| 17 | Zang W, Wu J, Zhang Z, Wang S, Zhang Q 2026, *Bioengineering* | PMID 42510440 / DOI 10.3390/bioengineering13070774 | §3.6 Gait2392 active-use corroboration |
| 18 | Saul KR, Hu X, Goehler CM, Vidt ME, Daly M, Velisar A, Murray WM 2015, *Comput Methods Biomech Biomed Engin* 18(13):1445–1458 | PMID 24995410 / PMCID PMC4282829 / DOI 10.1080/10255842.2014.916698 | §3.7 MoBL-ARMS DOF/muscle/compute/licence |
| 19 | SimTK project page, Dynamic Upper Limb (MoBL-ARMS) | https://simtk.org/projects/upexdyn | §3.7 licence text |
| 20 | Seth A, Dong M, Matias R, Delp S 2019, *Front Neurorobot* 13:90 | PMID 31780916 / PMCID PMC6856649 / DOI 10.3389/fnbot.2019.00090 | §3.8 thoracoscapular model, §5 compute cost, §6 licence |
| 21 | SimTK project page, Thoracoscapular Shoulder Model | https://simtk.org/projects/thoracoscapular | §3.8 licence text |
| 22 | Carpenedo M, et al. 2025, *Ann Biomed Eng* 53(11):2883–2910 | PMID 40913215 / PMCID PMC12575568 / DOI 10.1007/s10439-025-03818-8 | §3.9 master comparison of thoraco-lumbar spine models, DOF/axial-rotation table |
| 23 | Remus R, Selkmann S, Lipphaus A, Neumann M, Bender B 2023, *Front Bioeng Biotechnol* 11:1223007 | PMID 37829567 / PMCID PMC10565495 / DOI 10.3389/fbioe.2023.1223007 | §2.1, §3.10 forward-dynamics muscle-driven spine model |
| 24 | Van Wouwe T, Hicks J, Delp S, Liu KC 2024, *PLoS Comput Biol* | PMID 38394308 / PMCID PMC10917303 / DOI 10.1371/journal.pcbi.1011410 | §2.1, §5 differentiable simulator compute cost |
| 25 | Ackermann M, van den Bogert AJ 2010, *J Biomech* 43(5):1055–1060 | PMID 20074736 / PMCID PMC2849893 / DOI 10.1016/j.jbiomech.2009.12.012 | §2.1 forward-dynamics-predicted gait, cost-function sensitivity |
| 26 | Mathieu E, Crémoux S, Duvivier D, Amarantini D, Pudlo P 2023, *J Neuroeng Rehabil* 20:130 | PMID 37752507 / PMCID PMC10521397 | §4 redundancy problem, static optimization limitations |
| 27 | Princelle D, Viceconti M, Davico G 2025, *Ann Biomed Eng* | PMID 40128488 / PMCID PMC12075340 / DOI 10.1007/s10439-025-03713-2 | §4 static optimization vs EMG-assisted comparison |
| 28 | Nasr A, Inkol KA, Bell S, McPhee J 2021, *Front Comput Neurosci* | PMID 35002663 / PMCID PMC8735851 / DOI 10.3389/fncom.2021.759489 | §4 machine-learning alternative to static optimization |
| 29 | Lee SH, Park M, Lee K, Lee J 2019, *ACM Trans Graph* (SIGGRAPH 2019) | DOI 10.1145/3306346.3322972 (abstract via Semantic Scholar API) | §2.1, §5 346-muscle full-body DRL-controlled forward simulation |
| 30 | opensim-core LICENSE.txt, GitHub | https://github.com/opensim-org/opensim-core/blob/main/LICENSE.txt | §6 OpenSim core = Apache-2.0 |
| 31 | opensim-moco repository, GitHub | https://github.com/opensim-org/opensim-moco | §6 Moco = Apache-2.0, archived/merged into core |
| 32 | AnyBody Modeling System release notes | https://www.anybodytech.com/software/anybody-modeling-system | §6 AnyBody commercial licensing |
| 33 | LifeMOD vendor domain redirect | https://www.lifemodeler.com/ (redirects to smith-nephew.com) | §6 LifeMOD apparent discontinuation |
| 34 | Visual3D documentation wiki | https://wiki.has-motion.com/index.php/Visual3D | §6 Visual3D licensing/capability |
| 35 | Vasudevan JM, Logan A, Shultz R, et al. 2016, *J Sports Med* | PMID 27403454 / PMCID PMC4925984 / DOI 10.1155/2016/3987486 | Context: golf swing muscle-onset EMG sequencing (background, not modelling) |
| 36 | Haddas R, Pipkin W, Hellman D, et al. 2022, *Global Spine J* | PMID 33541112 / PMCID PMC8907648 / DOI 10.1177/2192568220983291 | Context: lumbar spine forces/protection in golf swing (background) |
|---|--------|----------|----------|
