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

*(Still pending: Hamner 2010 running model, Gait2392, MoBL-ARMS upper-extremity model,
Thoracoscapular Shoulder Model, Christophy 2012 and Bruno 2015 lumbar models — fetching
next.)*

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
