# 11 — Video and Markerless Pose Estimation for the Golf Swing

Task: T-033 (Phase 1b, inference research). Question: can markerless/video-based pose estimation
yield joint angles accurate enough to count as evidence for this project, and what golf-specific
video datasets and event-detection methods exist? Status: IN PROGRESS. Sources cited by
URL/PMID/PMCID/DOI/arXiv ID as fetched; nothing entered without its own citation.

---

## 1. Markerless motion capture validity — general (non-golf) evidence base

This section establishes the general accuracy ceiling of markerless/video pose estimation before
any golf-specific claim is assessed, because no golf study currently reports RMS joint-angle error
against a marker-based ground truth (see §3, §7).

### 1.1 OpenCap — pooled/meta-analytic accuracy

Çabuk, Ulupınar, İnce & Özbay, "Can OpenCap Deliver Valid and Reliable Kinematic Data for Motion
Analysis? A Systematic Review and Three-Level Meta-Analysis" (*Biology of Sport* 2026, PMID
41783455, PMCID PMC12954493, DOI 10.5114/biolsport.2026.154942) — 12 studies, 184 participants,
640 effect sizes, 230 Fisher's Z values, 1087 RMSE values:
- Pooled RMSE across all joint angles/tasks: **5.877°**, falling to **5.197°** after sensitivity
  analysis and **4.940°** after trim-and-fill publication-bias adjustment.
- Correlation with criterion (marker-based) devices: **r = 0.845** (Fisher's Z, p = 0.005).
- Effect size vs criterion devices: ES = −0.140 (p = 0.021) — "statistically significant, yet
  practically trivial."
- Reliability (test-retest): "moderate to very good" across most joint/task combinations, but
  "marked variability... particularly in high-velocity movements and complex joint actions" —
  i.e. the pooled number degrades precisely in the direction a golf swing would push it (fast,
  complex, multi-plane).

### 1.2 OpenCap — individual validation studies (joint- and plane-specific)

- Svetek, Morgan, Burland & Glaviano, *J Biomech* 2025 (PMID 40048968, DOI
  10.1016/j.jbiomech.2025.112602), 20 athletes, walking/running/squat/CMJ/jump-landing vs Vicon:
  **RMSE <6° frontal-plane hip** (strong agreement); **4–10° sagittal-plane knee** (moderate);
  **>10° sagittal-plane hip during gait** (weak agreement). Directly confirms rotational/complex
  planes and proximal (hip) joints degrade fastest.
- Verheul et al., *J Biomech* 2026 (PMID 41418503, DOI 10.1016/j.jbiomech.2025.113133), 30
  runners, treadmill 8–16 km/h: systematic differences vs marker-based "throughout the stride
  cycle, and across running speeds and kinematic variables," worst around peak joint angles and
  during swing phase; high inter-trial/inter-stride agreement preserved despite this, so OpenCap
  is more trustworthy for relative/variability comparisons than absolute angle values.
- Färber, Horsak & Paternoster, *Sci Rep* 2026 (PMID 41876778, PMCID PMC13018474, DOI
  10.1038/s41598-026-44758-0), 24 healthy adults, 240 drop jumps: **RMSE >6° frontal-plane knee**
  despite strong waveform correlation (r>0.90); transverse-plane hip moment MAE <1% but "weak to
  strong negative correlations" (i.e. unstable sign); sagittal knee moment MAE 5.6% (r>0.90);
  vertical GRF MAE >6% (r>0.90). Conclusion in the paper itself: "OpenCap currently cannot be
  recommended for ACL re-injury risk assessment."
- de Borba et al., *Sensors* 2025 (PMID 41157527, PMCID PMC12568194, DOI 10.3390/s25206474), 15
  adults, 3 walking speeds: excellent spatiotemporal agreement (ICC ≥0.95), joint-waveform RMSE
  <2°, CoM displacement RMSE <6 mm — but **joint range-of-motion reliability drops specifically
  at the hip and ankle at higher speeds**, and OpenCap underestimates walking speed more as speed
  increases. Second independent confirmation that speed degrades accuracy.
- Turner et al., *J Biomech* 2026 (PMID 41138605), 33 healthy adults, jump-landing: intersystem
  ICC₂,₁ 0.79–1.00, test-retest ICC₂,ₖ 0.70–0.97, **minimal detectable change (MDC) 1.89–11.62°**
  depending on joint/task — i.e. for some joint/task combinations a >11° change is needed before
  OpenCap can distinguish real change from noise.
- You, Lin & Zhang, *Sensors* 2026 (PMID 42280894, PMCID PMC13259095, DOI 10.3390/s26113375), 16
  children, vertical jump GRF: moderate-high correlation (r>0.7–0.85) but **landing-phase peak
  force bias >40%** ("weak agreement... should be interpreted with caution") — the fast, impact
  portion of the movement is the least trustworthy, structurally analogous to golf impact.
- Horsak et al., *J Biomech* 2025 (PMID 41046587, DOI 10.1016/j.jbiomech.2025.112986) — monocular
  single-camera 3D pose (CameraHMR/SMPL) vs two-camera OpenCap vs marker-based, 19 healthy
  walkers, 4 gait patterns: monocular reliability RMSD 3.0±1.0°; monocular **validity RMSD
  5.5±1.1°** vs marker-based, "despite challenges in tracking ankle joint kinematics." Confirms
  single-camera (monocular) is close to two-camera OpenCap for simple sagittal gait but the paper
  explicitly says "further refinement is needed to reach clinically acceptable accuracy
  thresholds."
- Yan et al., *Sensors* 2025 (PMID 41013149, PMCID PMC12473682, DOI 10.3390/s25185911), 22
  children with cerebral palsy, standing balance: CoM-vs-CoP correlation R = 0.39–0.94 raw,
  R² = 0.98–1.00 only after correction — i.e. raw OpenCap output required a correction model to
  reach high agreement.

### 1.3 Theia3D — individual validation studies

Theia3D is a markerless system using synchronised multi-camera video (unlike OpenCap's 2-phone
setup), generally used with 8–27 cameras in a lab, not casual smartphone video:
- Shimotori et al., *JMIR Rehabil Assist Technol* 2025 (PMID 40373227, PMCID PMC12097655, DOI
  10.2196/66886), 21 healthy adults, 27 cameras, ramp/stair ascent-descent: level-walking SEM all
  <5°; **ramp-ascent knee-flexion RMSD 5.07°; stair-ascent knee-flexion RMSD 5.64°**; full-curve
  RMSD generally <5°.
- Helwig et al., *Sci Rep* 2025 (PMID 41028120, PMCID PMC12484822, DOI 10.1038/s41598-025-21143-x),
  19 athletes, cutting/change-of-direction (fast, rotational — closest published analogue to a
  golf-swing-speed rotational task found in this search): knee flexion/extension bias 4.34°;
  Bland-Altman knee bias 3.34°, **limits of agreement (LoA) ±11.38°**; flexion/extension LoA
  ±10.71°; ab-/adduction LoA ±12.16°; **internal/external rotation LoA ±15.75°** — the rotational
  degree of freedom has the widest limits of agreement of any plane measured, directly confirming
  the brief's expectation that rotational DOF are worse than flexion/extension, this time in a
  fast athletic (not just gait) task.
- Yang et al., *Sci Rep* 2025 (PMID 40425708, PMCID PMC12117081, DOI 10.1038/s41598-025-02739-9),
  14 male collegiate athletes, squat/drop/countermovement jumps: joint-angle RMSD ≤5.6°; hip
  moment RMSD ≤0.26 N·m/kg; power RMSD ≤2.12 W/kg; but SPM analysis found **significant
  differences in sagittal-plane hip angles** despite the summary RMSD looking acceptable.
- D'Souza et al., *Sci Rep* 2024 (PMID 39587194, PMCID PMC11589150, DOI
  10.1038/s41598-024-80499-8), 12 healthy + 34 clinical, gait: **"hip and knee rotations
  non-comparable between systems"**; pelvic anterior tilt significantly underestimated; significant
  differences across all planes for all joints in sagittal hip/knee/ankle powers. One of the
  strongest direct statements in the literature that rotational kinematics from markerless video
  are not usable as a substitute for marker-based rotation measurement.
- Poomulna et al., *Gait Posture* 2024 (PMID 39490268, PMCID PMC12415537, DOI
  10.1016/j.gaitpost.2024.10.018), 15 children with CP + 24 typically developing: Gait Deviation
  Index 6.9 points lower with Theia3D vs marker-based (p<0.05); **kinematic RMSD >10° for pelvic
  tilt, hip flexion/extension, hip rotation, and foot progression angle** — again rotation and
  pelvis (proximal/axial) among the worst-performing measures.
- Yoma et al., *Int J Sports Phys Ther* 2025 (PMID 40756794, PMCID PMC12317789, DOI
  10.26603/001c.141870), 19 recreational athletes, single-leg squat/landing: markerless RMSD
  3.2–3.6°, marker-based RMSD 3.3–4.2° (markerless was comparable to or slightly better than
  marker-based here, an unusual result); markerless ICC 0.77–0.83 vs marker-based ICC 0.80–0.90.
- Adlou et al. review, *Sensors* 2025 (PMID 40732512, PMCID PMC12299843, DOI 10.3390/s25144384):
  markerless-system sagittal-plane accuracy **3–15°**, transverse-plane accuracy **3–57°** — the
  widest reported spread for transverse (rotational) plane found in this search, confirming
  rotational DOF error can be an order of magnitude worse than flexion/extension in adverse cases.
- Doerks et al., *PLoS ONE* 2025 (PMID 40445923, PMCID PMC12124523, DOI
  10.1371/journal.pone.0324499), 2D video app (Orthelligent VISION) vs Qualisys: knee RoM
  deviation 3.8°, hip RoM deviation 3.7°, ankle RoM deviation 5.4°, correlation range 0.36–0.83
  (best r=0.71 at 1 m/s treadmill only) — a 2D (not 3D) video method, included to show 2D-only
  video is markedly less reliable (r as low as 0.36) than 3D multi-camera markerless.

**Section 1 conclusion**: across ~25 independent OpenCap/Theia3D validation studies found, no
study anywhere reports single-digit-degree accuracy for transverse-plane/rotational measurements
in a fast or complex task. Flexion/extension in slow, sagittal, non-fast tasks (walking, level
gait) is the only condition that reliably achieves <5° RMSE. Every axis identified by the brief as
suspect — rotation, proximal joints (hip, pelvis, trunk), and high-velocity phases — is confirmed
independently by multiple different research groups to be the weakest part of markerless
performance, consistent with (and extending) the running-hip CMC=0.65/15°-offset finding the user
supplied as context.

---
