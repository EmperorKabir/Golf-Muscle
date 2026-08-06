# 08 — Musculoskeletal Simulation of the Golf Swing: Can Muscle Activation Drive Motion?

Task: T-030 (Phase 1b). Question: does a published musculoskeletal model of the golf swing
exist; has anyone driven a golf-swing simulation forward from muscle activation
(activation → force → moment → motion); what generic full-body models could be adapted;
what are the trunk-axial-rotation, redundancy, computational-cost, and licensing
implications for a free public Android app. Status: IN PROGRESS — building incrementally,
one source at a time. Nothing entered without its own citation (URL/PMID/DOI).

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

*(sources pending — no golf-specific hit yet located; searching adjacent ballistic/rotational
sports and generic OpenSim forward-dynamics/CMC literature for transferable evidence)*

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

*(sources pending)*

## 5. Computational cost — real-time on a phone, or precomputed offline?

*(sources pending)*

## 6. Licensing of every model / dataset / software mentioned

*(sources pending)*

---

## Running source log

| # | Source | URL/PMID/DOI | Used for |
|---|--------|----------|----------|
