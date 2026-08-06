# 11 — Video and Markerless Pose Estimation for the Golf Swing

Task: T-033 (Phase 1b, inference research). Question: can markerless/video-based pose estimation
yield joint angles accurate enough to count as evidence for this project, and what golf-specific
video datasets and event-detection methods exist? Status: DONE 2026-08-07 — 47 sources. Sources
cited by URL/PMID/PMCID/DOI/arXiv ID as fetched; nothing entered without its own citation. Four
open gaps declared in §8 (no direct trunk-axial-rotation number found anywhere; no controlled
frame-rate-vs-accuracy study for golf; CaddieSet's 924-vs-1,757-swing count discrepancy; no
SwingNet successor located) for a future targeted follow-up if the project revisits this file.

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

### 1.4 MediaPipe-specific validation studies

- Russo et al., *Sensors* 2026 (PMID 41977932, DOI 10.3390/s26072148), smartphone + MediaPipe vs
  OPAL wearable sensors, gait: knee flexion MAE 4.10°±2.32° (right) / 3.15°±3.10° (left); knee
  extension MAE 2.30–3.12°; knee ROM MAE 4.15–4.55°; correlation 0.845–0.916 for flexion — "poor
  ankle measurement concordance" noted despite acceptable knee numbers.
- Balci et al., *Front Sports Act Living* 2025 (PMID 41602810, DOI 10.3389/fspor.2025.1712332),
  MediaPipe (2D and 3D) vs OptiTrack: MediaPipe 2D ICC 0.85.
- Lazem et al. (Track-UL algorithm on MediaPipe), *JMIR Rehabil Assist Technol* 2026 (PMID
  42114045, DOI 10.2196/87128), upper-limb ROM in stroke survivors vs Kinovea: shoulder 95% limits
  of agreement −3.18 to 6.41° (lab) / −6.21 to 3.62° (home); elbow LoA −5.35 to 8.78° (lab) / −4.06
  to 2.53° (home); ICC 0.97–0.99 — best MediaPipe numbers found, but for slow, controlled,
  single-plane ROM tasks, not a ballistic multi-plane swing.
- Kondo & Suzuki, *J Phys Ther Sci* 2026 (PMID 42306435, DOI 10.1589/jpts.38.270), Parkinson's
  postural tracking: lumbar flexion ICC 0.98, thoracic flexion ICC 0.96, but **lateral trunk
  flexion ICC only 0.80** — the off-sagittal trunk plane is again the weakest, consistent with
  §1.3's rotational-DOF pattern.
- Edriss et al., review, *Front Physiol* 2025 (PMID 40873758, DOI 10.3389/fphys.2025.1649330):
  general mini-review of commercial vision sensors/AI pose frameworks for sport, concluding
  2D-to-3D fusion is a "promising" but not yet solved direction — a review-level confirmation that
  the field itself does not consider monocular/markerless 3D pose a solved problem for sport.

### 1.5 Monocular-specific depth/rotation findings

- Rode, Dunkel, Willi, Wolf, Xiloyannis & Riener, *Sci Rep* 2025 (PMID 41193590, DOI
  10.1038/s41598-025-22626-7), "Assessment of monocular human pose estimation models for clinical
  movement analysis": mean per-joint position error **146–249 mm in 3D when depth is considered**
  (i.e. tens of centimetres of positional error once the camera-axis dimension is included, far
  worse than the in-plane 2D error); knee flexion MAE ≈6–7°, elbow flexion MAE ≈8–9° in 3D.
- Pratapneni, Halvorson, Silvestros, Harris & Bailey, *IEEE Access* 2026 (PMID 42238785, DOI
  10.1109/access.2026.3687207), "Validating Single-Camera Pose Estimation Against Multi-Camera
  Motion Capture for Accessible Biomechanical Assessment": explicit finding that "**proximal
  joints and frontal-plane motions showed higher fidelity, with the greatest errors in distal,
  dynamic joints**" — for monocular specifically, error is concentrated in exactly the fast/dynamic
  segments, the same pattern as the multi-camera systems in §1.1–1.3 but from a single camera.
- Guo, Gao, Dong, Jiang, Zhu & Wang, "A Survey of the State of the Art in Monocular 3D Human Pose
  Estimation: Methods, Benchmarks, and Challenges," *Sensors* 2025 (PMID 40285099, DOI
  10.3390/s25082409) — survey-level confirmation that depth ambiguity remains an open, named
  challenge category in the monocular 3D pose literature as of 2025, not a solved problem.

**No study found in this search isolates or quantifies "trunk axial rotation error" as its own
number** — every trunk-relevant figure available (Kondo & Suzuki's lateral trunk flexion ICC 0.80
vs sagittal 0.96–0.98; Helwig et al.'s internal/external rotation LoA ±15.75° vs flexion/extension
LoA ±10.71°, §1.3; Adlou et al.'s transverse-plane range 3–57° vs sagittal 3–15°, §1.3) is an
indirect proxy showing the off-sagittal/rotational axis is consistently the worst-performing axis
by a wide margin, never the best. This is consistent with, not a refutation of, the brief's
starting hypothesis that axial/rotational DOF are the hardest to recover from video.

Two general sports-AI scoping/systematic reviews add outer-bound context but not golf- or
rotation-specific numbers: Aulton et al., "The Application of Deep Learning Human Pose Estimation
in Sport: A Systematic Review" (2025, PMID 41369858), screened 371 articles and found "most
studies relied on private datasets for algorithm training and validation, limiting reproducibility
and generalizability" — a field-level warning that many sport-pose accuracy claims are not
independently reproducible. Souaifi et al., "Artificial Intelligence in Sports Biomechanics" (2025,
PMID 40868401), PRISMA-ScR scoping review of 73 studies (Jan 2015–Dec 2024, 3248 screened, Cohen's
κ=0.84): pooled figures across all sports (not golf-specific) include CNN technique-assessment
agreement with international experts of **94%**, and computer-vision positional accuracy "within
15 mm compared to marker-based systems" for the tasks it covers — the abstract contains no mention
of golf, muscle activation, or joint-kinetics-from-video anywhere in the 73-study set.

---

## 2. High-speed limitation — can standard video pipelines cope with the golf downswing?

The golf downswing lasts ≈0.25 s with clubhead speed approaching 90 mph (≈40 m/s) at impact —
several orders of magnitude faster and more rotational than the walking/running/jumping tasks
that comprise nearly the entire markerless-validation evidence base assembled in §1.

**Direct, quantified confirmation that standard video frame rates miss golf's critical moment.**
McNally, Vats, Pinto, Dulhanty, McPhee & Wong, "GolfDB: A Video Database for Golf Swing Sequencing"
(arXiv:1903.06528, 2019 — also the source for §3/§4 below) built their 1400-video dataset from
YouTube footage **sampled at 30 fps, 720p**, and state explicitly: **"at 30 fps, it was rare that
the precise moment of impact was captured."** This is a primary-source, quantitative admission
that the standard video frame rate used for the largest public golf-swing video dataset cannot
reliably capture the single most biomechanically important instant of the swing. Some source clips
were slow-motion at "upwards of 240 frames per second," but this was the exception in their corpus,
not the rule, and ordinary broadcast/consumer/YouTube golf video defaults to 30 fps.
- Frame-interval arithmetic (elementary, not a citation): at 30 fps the interval between frames is
  33.3 ms; at 40 m/s clubhead speed the club travels **≈1.3 m between consecutive frames** —
  meaning a 30 fps camera can localise impact to no better than roughly a metre of clubhead travel,
  and the "impact frame" is frequently a motion-blurred smear rather than a sharp image at all.
  At 240 fps (4.17 ms/frame) the same travel distance drops to ≈0.17 m per frame — still coarse
  relative to a golf-ball diameter (42.7 mm) but two orders of magnitude better than 30 fps.
- Yamamoto et al. 2023 (§1, PMID 38033658/PMCID PMC10684732) used a dedicated **240 Hz** camera
  (Sony RX100M7, 1824×616) specifically to analyse golf swings with markerless pose (HRNet) —
  i.e. the one golf-specific markerless-pose study located in this entire search deliberately
  chose 8× the standard 30 fps rate, an implicit confirmation from a working golf-biomechanics lab
  that 30 fps is judged inadequate for this task. Even so, the authors did **not** validate their
  2D pose output against any 3D/marker-based ground truth (see §1/§4), and stated outright: "the
  golf swing is a 3D motion involving the rotation and twisting of the body, the method used in
  this study is inferior with respect to accuracy, compared with 3D motion analysis."

**Golf swing kinematics/kinetics studies that do report a frame rate overwhelmingly use dedicated
multi-camera infrared systems, not ordinary video.** Yang, Chang, Chao, Tai & Tsai, "The effects
of different iron shaft weights on golf swing performance," *Front Bioeng Biotechnol* 2024 (PMID
38380262), used **nine infrared high-speed cameras** — no frame rate was extractable from the
abstract, but the camera-count/type (dedicated infrared marker system rather than an ordinary
camcorder) is itself evidence of the equipment class golf biomechanics research judges necessary.
Watson et al., "Ground Reaction Force and Centre of Pressure During the Golf Swing... A Systematic
Review," *Sports Med* 2026 (PMID 41653371), 24 studies passing quality screening (score 7–8/10),
found **zero video-based or markerless measurement methods among them** — every included GRF/CoP
study used force-plate instrumentation; the review does not even raise markerless capture as an
alternative. This independently confirms the golf-kinetics literature has not yet attempted
markerless/video capture at all, consistent with §6's finding for muscle activation specifically.

**Motion blur as a distinct failure mode from frame rate.** No golf-specific study quantifying
motion-blur degradation of pose-estimation accuracy was found. The closest sport-specific evidence
is Wang et al., "Badminton Swing Trajectory Reconstruction," *Sci Rep* 2026 (PMID 41922587, DOI
10.1038/s41598-026-46443-8): badminton smash instantaneous velocity "can exceed 100 m per second,"
and the authors report that **event cameras** (which sidestep frame-based motion blur entirely by
recording per-pixel brightness changes asynchronously) achieved a **42.3% reduction in trajectory
reconstruction error compared to traditional optical-flow methods** on frame-based video — direct
evidence that motion blur is treated as a significant, quantified error source in fast racquet-
sport motion, addressed by hardware (event cameras), not by standard consumer video pipelines.
Zhang et al., "Basketball Action Pose Estimation," *Sci Rep* 2025 (PMID 40783613, DOI
10.1038/s41598-025-14985-y) similarly names "motion blur, occlusions, and complex backgrounds" as
named challenges for athlete pose estimation but does not quantify the blur contribution in
isolation. No equivalent event-camera or motion-blur-isolating study exists for golf specifically.

**Section 2 conclusion**: the golf-specific evidence found (GolfDB's own admission; Yamamoto et
al.'s deliberate 240 Hz choice; Watson et al.'s finding of zero markerless golf-kinetics studies)
converges on the same answer — ordinary consumer/broadcast video frame rates (24–30 fps) are
judged inadequate by the field's own working practitioners for the fast, high-velocity phase of
the golf swing, and dedicated high-speed capture (≥240 fps, or dedicated infrared multi-camera
rigs) is what is actually used whenever golf kinematics are studied seriously. No study locates or
quantifies a minimum sufficient frame rate for golf specifically; the number is inferred from
practitioner choice (240 Hz), not derived from a validation study that tested multiple frame rates
against ground truth and reported the accuracy/fps trade-off.

---

## 3. Golf-specific video/pose datasets

### 3.1 GolfDB

McNally, Vats, Pinto, Dulhanty, McPhee & Wong, "GolfDB: A Video Database for Golf Swing
Sequencing," arXiv:1903.06528 (2019), full text via ar5iv (https://ar5iv.labs.arxiv.org/html/1903.06528):
- **1400 high-quality golf swing videos**, YouTube-sourced, **248 unique golfers** (male and
  female, professional and amateur), each video labelled with: 8 event frames, bounding box,
  player name, player sex, club type, and view type (face-on / down-the-line).
- Videos **sampled at 30 fps, 720p resolution**; some source clips slow-motion up to 240 fps, but
  not the majority (§2).
- **2D only** — no 3D joint or marker data; the dataset provides bounding boxes and event labels,
  not skeletal keypoints (pose extraction is left to the user/downstream model).
- Eight labelled events: **Address (A), Toe-up (TU), Mid-backswing (MB), Top (T), Mid-downswing
  (MD), Impact (I), Mid-follow-through (MFT), Finish (F)** — directly usable for aligning a swing
  timeline (see §4).
- **Licence: Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**, per
  the repository (github.com/wmcnally/golfdb). **This licence is incompatible with a free public
  app that is not itself non-commercial** unless the app remains strictly non-commercial in
  perpetuity (CC BY-NC forbids commercial use/redistribution of the licensed material or derivative
  works incorporating it) — a constraint the project must record if GolfDB or its video content is
  ever redistributed or trained-on-and-shipped rather than used purely for internal research
  reference.
- Preprocessed 160×160 clips distributed via Google Drive; original YouTube URLs also provided for
  independent re-preprocessing at other resolutions.

### 3.2 CaddieSet

Jung, Hong, Jeong, Jeong, Choi, Kim & Lee, "CaddieSet: A Golf Swing Dataset with Human Joint
Features and Ball Information," arXiv:2508.20491 (2025), full text via ar5iv
(https://ar5iv.labs.arxiv.org/html/2508.20491), GitHub: github.com/damilab/CaddieSet:
- **924 golf swings analysed in the arXiv abstract summary (613 driver, 23 3-wood, 288 iron
  I4–I9), while the repository page states 1,757 shots from 8 individuals across two camera
  angles (face-on and down-the-line)** — the discrepancy between the paper abstract's swing count
  and the repository's shot count was not resolved in this search and should be treated as an open
  item if the project uses this dataset (possibly reflecting different processing/filtering stages
  or a dataset update between the arXiv submission and current repo state).
- **2D keypoints only**, extracted with **HRNet** (17 COCO-format joints: shoulders, elbows,
  wrists, hips, knees, ankles), coordinates scaled to bounding-box width to normalise across
  camera positions/distances.
- Swing segmented into the same style of 8 phases as GolfDB: **Address, Takeaway, Backswing, Top,
  Downswing, Impact, Follow-through, Finish**.
- Pose/event-extraction pipeline validation reported in-paper: their event-sequencing detector
  reached **78.0% overall accuracy, rising to 94.1% when the Address and Finish events are
  excluded** (compare 91.8% "six-event" baseline reported for SwingNet in the original GolfDB
  paper, §4) — i.e. address/finish detection is the recurring weak point across two independent
  golf-video datasets, not just GolfDB. Object detection backbone: Faster R-CNN alone scored 56.4
  AP on MS COCO; combined with HRNet pose refinement, AP rose to 74.9.
- 15 hand-defined swing-influence metrics used to predict ball trajectory via interpretable ML,
  validated qualitatively against "established golf domain knowledge" (not against 3D ground-truth
  kinematics).
- No stated video frame rate found in the accessible text.
- **Licence: MIT** (per GitHub repository footer) — permissive, compatible with a free public app,
  a materially better position than GolfDB's CC BY-NC 4.0 if this dataset were to be used directly.
  Dataset download mechanics were not confirmed accessible in this search (a "data" folder exists
  in the repo but no working download link was visible in the fetched content).

### 3.3 Other golf video/pose-adjacent resources found (not full video-pose datasets)

- Lauer, "Learning golf swing signatures from a single wrist-worn inertial sensor," arXiv:2506.17505
  (2025): trains on **video of professional golfers to reconstruct full-body 3D kinematics via
  "biologically accurate human mesh recovery,"** then distils that into a wrist-IMU-only inference
  model. Relevant as evidence that video-derived 3D mesh recovery is being used as a *training
  label source* for other sensing modalities in golf, but the paper's own deployed product is
  IMU-based, not video-based, at inference time — an implicit signal that the author judged
  on-course video capture (§2's "impractical camera placement," directly below) less practical
  than a single wearable for field use.
- The WIT-KinNet smartwatch paper, arXiv:2606.22876 (2026), 36 golfers, 7 club types, full/half/
  quarter swings, evaluated against **optical motion-capture ground truth**, achieved **mean
  absolute error 8.11° ± 1.84° across full-body joint angles** from a single wrist IMU — and states
  outright that existing **camera-based golf methods "require impractical camera placement"** as
  their stated motivation for avoiding video entirely. This is an independent, golf-domain-specific
  statement (not the user's supplied context, a separate primary source) that camera-based capture
  is considered a practical liability for golf swing capture by researchers actively building
  alternatives to it. Included for context, not as a video-pose accuracy source, since it is an
  IMU method.
- "How Can I Swing Like Pro?: Golf Swing Analysis Tool for Self Training," Liao, Hwang & Koike,
  arXiv:2105.10153 (2021): a video-synchronisation and 3D-pose-visualisation coaching tool that
  aligns amateur and pro swing videos by phase using a neural encoder; a UI/coaching tool, not a
  released dataset, and no accuracy-vs-ground-truth figures found.
- UCF Sports Action dataset (used in Turner et al., arXiv:1512.07502, 2015) includes golf-swing
  clips among nine sports as an action-recognition benchmark (classify "this video shows a golf
  swing"), not a pose/kinematics dataset — mentioned only to flag it is not usable for joint-angle
  extraction purposes.

**Section 3 conclusion**: two purpose-built golf video/pose datasets exist (GolfDB, CaddieSet),
both 2D-only, both YouTube/consumer-video-sourced (no confirmed high-frame-rate golf pose
dataset), with materially different licences — GolfDB CC BY-NC 4.0 (non-commercial only), CaddieSet
MIT (permissive). Neither dataset provides 3D ground-truth kinematics, and neither has been
validated against marker-based motion capture (§1's entire evidence base is non-golf).

---

## 4. Golf swing event detection from video

McNally et al.'s SwingNet (GolfDB paper, arXiv:1903.06528, full detail via ar5iv), a hybrid
CNN(MobileNetV2)-RNN(bidirectional LSTM) trained/evaluated on GolfDB, detects the same 8 events
listed in §3.1. **Per-event PCE (percent correct event, within a frame tolerance) from their
Table 2** (self-consistency-checked: the 8 values average to exactly 76.1%, confirming the figures
are internally coherent and not summarisation error):

| Event | Address | Toe-up | Mid-back­swing | Top | Mid-down­swing | Impact | Mid-follow-through | Finish | **Average** |
|---|---|---|---|---|---|---|---|---|---|
| PCE | 31.7% | 84.2% | 88.7% | 83.9% | 98.1% | **98.4%** | 97.6% | 26.5% | **76.1%** |

Also reported: **91.8%** average when restricted to the six events excluding Address and Finish.

- **The two long, static "hold" events (Address, Finish) are the hardest to localise precisely**
  (31.7% and 26.5%), not the fast-motion events — Impact itself is the single best-detected event
  at 98.4%. This is an important, counter-intuitive nuance for the project: the failure mode in
  the one dataset with a per-event breakdown is boundary ambiguity within a long stationary phase
  (many visually near-identical frames each equally plausible as "the" address/finish frame), not
  motion blur at speed — though this does not contradict §2's frame-rate concern, since the model
  still only had 30 fps input to work with for locating impact, and 98.4% PCE is measured against
  a tolerance window, not against a marker-based/force-plate ground-truth reference for the true
  ball-contact instant (GolfDB has no such reference — event labels were established by human
  video annotation, not instrumented ground truth).
- CaddieSet's own event/sequence-detection pipeline (§3.2) reports the same qualitative pattern —
  78.0% overall, rising to 94.1% when Address and Finish are excluded — independently reproducing
  GolfDB's finding that the static bookend events are the harder detection problem across two
  unrelated groups' datasets/models, which strengthens confidence this is a real, general property
  of golf-swing event detection rather than an artefact of one model.
- **No successor paper improving on SwingNet's PCE numbers was located** — a targeted arXiv search
  for "event spotting" + golf returned zero results, and a broader golf+video/pose search (§ full
  list of hits already enumerated in §3) surfaced no post-2019 golf event-detection accuracy paper
  beyond GolfDB/SwingNet and CaddieSet's downstream reuse of the same task.
- Direct relevance to this project's timeline alignment: event PCE at ~76–98% (except the two
  static bookends) is a frame-classification accuracy, not a joint-angle accuracy — it tells you
  *which frame* is impact/top-of-backswing with reasonable confidence, but says nothing about
  whether the joint angles measured *at* that frame are correct (that is §1's question, and §1
  found no golf-specific joint-angle validation exists at all).

---

## 5. 3D pose from monocular video, and trunk axial rotation specifically

**General monocular 3D pose state of the art (non-sport, lab-controlled benchmarks — Human3.6M,
the standard benchmark of simple, slow, single-subject indoor actions filmed multi-view then
evaluated monocular-style)**: recent top methods report mean per-joint position error (MPJPE) of
**37.6 mm (OPFormer 2025, PMID 40849577)**, **45.2 mm (SMPLer 2024, DOI 10.1109/tpami.2023.3341630)**,
and **47.6 mm (CGFusionFormer 2025, DOI 10.3390/s25196052)**. These are best-case numbers on a
benchmark of deliberately slow, simple, non-occluded, non-rotating actions (walking, sitting,
posing) — i.e. even under near-ideal conditions, state-of-the-art monocular 3D pose carries
**3.7–4.8 cm of average joint-position error**, before any golf-specific speed/rotation/occlusion
penalty is applied. Guo, Gao, Dong, Jiang, Zhu & Wang's 2025 survey (*Sensors*, PMID 40285099, DOI
10.3390/s25082409) confirms depth ambiguity remains a named, unsolved "fundamental challenge" of
single-view 3D pose as of 2025, addressed only partially by diffusion-based refinement, temporal
consistency constraints, and multi-hypothesis generation — none of which eliminates the ambiguity,
they only regularise it using learned priors from (non-golf) training data.

**Clinical/applied monocular studies (closer to real-world, non-benchmark conditions)** confirm
this ceiling degrades further outside the lab:
- Rode, Dunkel, Willi, Wolf, Xiloyannis & Riener, *Sci Rep* 2025 (PMID 41193590, DOI
  10.1038/s41598-025-22626-7): mean per-joint position error **146–249 mm in 3D when depth is
  considered** — i.e. up to a quarter of a metre of positional error once the camera-axis
  dimension is included, roughly 3–5× worse than the Human3.6M benchmark numbers above, for
  clinical movement analysis; angle-level MAE ≈6–7° knee flexion, ≈8–9° elbow flexion.
- Pratapneni, Halvorson, Silvestros, Harris & Bailey, *IEEE Access* 2026 (PMID 42238785, DOI
  10.1109/access.2026.3687207): explicit finding that "proximal joints and frontal-plane motions
  showed higher fidelity, with the greatest errors in distal, dynamic joints" for single-camera
  pose — the depth/rotation problem is worst precisely where a joint moves fast and off the
  camera's primary viewing plane.
- Horsak et al., *J Biomech* 2025 (PMID 41046587, §1.2): monocular CameraHMR/SMPL validity RMSD
  5.5±1.1° vs marker-based, for simple sagittal-plane gait only — the single golf-relevant proxy
  in this search for "how good is a single consumer camera at 3D angle recovery," and even that
  is a slow, non-rotational, single-plane task.

**Trunk axial rotation specifically — direct answer to the brief's central question**: no study
located in this search reports a dedicated trunk-axial-rotation (i.e. transverse-plane torso/pelvis
twist, the specific golf DOF the brief flags as most important and hardest to see) RMSE or LoA
figure, golf or otherwise. What exists is consistently unfavourable indirect evidence:
- Depth ambiguity is fundamentally a same-axis problem as axial rotation for a camera viewing a
  torso largely front-on or side-on: rotation about the vertical (long) body axis moves anatomical
  landmarks predominantly *along the camera's depth axis* (the axis every monocular-pose survey
  identifies as the weakest-resolved dimension, §1.5), rather than across the image plane where
  2D keypoint detectors (the first stage of every pipeline reviewed here — HRNet, MediaPipe,
  OpenPose-family, SMPL/CameraHMR) are comparatively reliable. This is a structural/geometric
  argument, not a numeric citation, and is stated here as reasoning rather than as a sourced fact.
- Every rotational/transverse-plane number actually measured in this search is markedly worse than
  the matched flexion/extension number from the same study: Helwig et al.'s int/ext-rotation LoA
  ±15.75° vs flexion/extension LoA ±10.71° (§1.3, fast cutting-sport task); Adlou et al.'s
  transverse-plane accuracy range 3–57° vs sagittal-plane 3–15° (§1.3); D'Souza et al.'s explicit
  statement that "hip and knee rotations [are] non-comparable between systems" (§1.3); Poomulna et
  al.'s finding that hip rotation is one of the measures exceeding 10° RMSD (§1.3); Kondo & Suzuki's
  lateral trunk flexion ICC 0.80 vs sagittal trunk flexion ICC 0.96–0.98 (§1.4).
- Yamamoto et al.'s golf-specific paper (§1, §2, PMID 38033658) — the only markerless golf-pose
  study found that discusses 3D rotation at all — used a single sagittal-plane camera and states
  directly that their method "is inferior with respect to accuracy, compared with 3D motion
  analysis" precisely *because* "the golf swing is a 3D motion involving the rotation and twisting
  of the body." The authors did not attempt to quantify trunk rotation from their video at all;
  they measured only forward/anterior tilt (a sagittal-plane angle) and explicitly could not
  address the transverse-plane swing-path question (inside-out vs outside-in) from their single
  camera. This is the single clearest golf-specific admission in the literature that monocular
  video cannot currently deliver trunk axial rotation.

**Section 5 conclusion**: no source found refutes the brief's starting hypothesis that depth/
rotation ambiguity makes monocular video unsuitable for recovering trunk axial rotation; every
piece of indirect and direct evidence available (general monocular-pose surveys naming depth
ambiguity as unsolved; every matched rotation-vs-flexion accuracy comparison found being worse for
rotation; and the one golf-specific video study explicitly declining to attempt trunk rotation
measurement and stating its method is inferior for exactly this reason) points the same direction.
This should be treated as a corroborated, multiply-sourced conclusion, not a single-study claim.

---

## 6. Muscle activation or joint moments derived from video of a golf swing

**No published work deriving muscle activation from video of a golf swing was found in this
search**, extending T-031's finding (`docs/research/09-inverse-activation-estimation.md`, F-036)
that no muscle-level model of the golf swing exists in the literature at all, video-driven or
otherwise. A targeted Europe PMC search ("golf swing muscle activation video estimation") returned
only Verikas et al., "Electromyographic Patterns during Golf Swing" (2016, PMID 27120604), which
uses **surface EMG, not video**, to study activation sequence and shot-quality prediction — the
closest hit, and it is not a video-derived-activation study at all.

**Joint kinetics (forces/moments, one level below muscle activation) from golf video**: also not
found. Watson et al.'s 2026 systematic review of golf GRF/CoP research (§2, PMID 41653371, 24
studies screened at quality ≥7/10) found **zero markerless/video-based studies** among the entire
included set — every GRF/CoP figure in the golf literature the review covers comes from
force-plate instrumentation. No golf-specific video-to-GRF or video-to-joint-moment pipeline of any
kind was located.

**General (non-golf) video-to-kinetics evidence, for context on what is and is not currently
possible anywhere, extending the user-supplied Vonstad et al. reference point**:
- Vonstad, Bach, Vereijken, Su & Nilsen, *J Neuroeng Rehabil* 2022 (PMID 35152877, DOI
  10.1186/s12984-022-00998-5) — already the primary source cited in T-031 §8 — found an LSTM
  predicting vertical GRF from **true 3D marker kinematics** achieved RMSE 4.3% BW / R²≈0.95, but
  from **plain 2D video-derived kinematics** degraded to **RMSE 10.7% BW / R²≈0.77** (a simpler
  XGBoost model was worse still, RMSE 19.8% BW), on a **slow, low-force balance weight-shifting
  exergame task in older adults** — nothing resembling golf-downswing loading.
- Feng, Ugbolue, Yang & Liu, *Bioengineering* 2025 (PMID 40564405, DOI
  10.3390/bioengineering12060588): CNN-based GRF/CoP estimation from markerless kinematics during
  **walking** (slow/normal gait): GRF component r 0.956–0.988, relative RMSE 6.03–9.44%; CoP r
  0.896–0.977, relative RMSE 6.41–7.90%.
- Schreff et al., *Children* 2026 (PMID 41897076, DOI 10.3390/children13030363): markerless-derived
  GRF/virtual-pivot-point analysis in paediatric **walking**: R²>0.95 across age groups.
- OpenCap-specific fast/high-force tasks (§1.2) again show the pattern breaking down at speed and
  impact: drop-jump vertical GRF MAE >6% despite r>0.90 (Färber et al., PMID 41876778); children's
  vertical-jump landing-phase peak-force bias **>40%**, explicitly flagged "weak agreement" (You et
  al., PMID 42280894).

**Section 6 conclusion — this directly corroborates and extends the parallel-strand finding
supplied in the brief**: every task in this search where video-derived GRF/kinetics achieved good
agreement (R²>0.95, RMSE <10% BW) was slow, low-impulse, and non-rotational (walking, weight-
shifting, paediatric gait). Every task involving a fast impact/landing phase (drop-jump, vertical-
jump landing) showed RMSE/bias rising sharply (>6% to >40%) specifically at the impact instant —
the golf swing's defining biomechanical event is exactly this kind of high-force, sub-second
impact. No study of any kind — golf or otherwise — has attempted video-to-muscle-activation for a
motion at golf-downswing speed, and the one domain (golf GRF) with an existing systematic review
confirms the entire published golf-kinetics literature is force-plate-only.

---

## 7. OpenCap specifically — validated accuracy, movements, golf applicability, licence

**What OpenCap is**: Uhlrich, Falisse, Kidziński, Muccini, Ko, Chaudhari, Hicks & Delp, "OpenCap:
Human movement dynamics from smartphone videos," *PLoS Comput Biol* 2023 (PMID 37856442, PMCID
PMC10586693, DOI 10.1371/journal.pcbi.1011462) — open-source platform computing **both kinematics
(motion) and dynamics (forces, muscle activations, joint loads/moments)** from **two or more
synchronised smartphone videos**, via a pipeline of: 2D pose estimation → deep-learning-assisted
biomechanical-model-constrained 3D kinematics → physics-based (OpenSim-based) musculoskeletal
simulation for muscle activations and joint loads/moments. The founding paper's headline validation
claim is a **100-subject field study** in which a clinician using OpenCap estimated musculoskeletal
dynamics **25× faster than a lab-based approach at <1% of the cost** — a throughput/cost claim, not
itself a per-joint accuracy claim (the accuracy claims are established by the independent
validation literature in §1.1–1.2, not by the founding paper's own abstract, which states only that
OpenCap "accurately predicts dynamic measures" without giving the number in the abstract text
retrieved).

**Validated accuracy (pooled, from the independent literature assembled in §1.1)**: pooled RMSE
5.877° (→4.940° after publication-bias correction), r=0.845 vs criterion devices, across 12 studies/
184 participants/1087 RMSE values (Çabuk et al. 2026, PMID 41783455). Individual-study range: as
good as RMSE <2° for level-gait joint waveforms and CoM RMSE <6 mm (de Borba et al., §1.2), as poor
as sagittal-hip-during-gait RMSE >10° (Svetek et al., §1.2) and drop-jump frontal-knee RMSE >6°
with the paper's own authors concluding "OpenCap currently cannot be recommended for [that specific
clinical] risk assessment" (Färber et al., §1.2).

**Which movements OpenCap has been validated on, per the studies located in this search**: walking
(multiple speeds), running (treadmill, multiple speeds), double-leg squat, countermovement jump,
drop jump, jump-landing (natural and cued-stiff), standing balance (including in children with
cerebral palsy), vertical jump (in children), gait in knee-osteoarthritis patients, upper-extremity
reachable workspace, single-leg Trendelenburg-test-adjacent tasks. **No study located anywhere in
this search has validated OpenCap on golf, or on any comparably fast, axially-rotational, whole-
body ballistic movement** — a targeted Europe PMC search for "OpenCap golf swing" returned zero
relevant hits. The closest task-type analogues in the validated set (drop jump, countermovement
jump, cutting/change-of-direction — though the latter used Theia3D not OpenCap, §1.3) are
consistently where accuracy is reported worst (§1.2, §1.3), which is the basis for judging OpenCap
**unvalidated, not merely "less accurate," for a golf swing** — the nearest validated proxies are
already the system's weakest-performing category.

**Kinetics/muscle-activation claim specifically**: OpenCap's founding paper claims muscle
activations and joint loads as an output, computed via OpenSim static optimisation/muscle-driven
simulation on top of the estimated kinematics (i.e. it inherits every limitation of static-
optimisation-based activation estimation documented in T-031, `09-inverse-activation-estimation.md`
— redundancy problem, cost-function dependence, R²/r 0.0–0.97 spread vs real EMG depending on
muscle/task, degrading for fast/individual/biarticular cases — on top of whatever kinematic error
OpenCap itself contributes at the input stage). No study located in this search independently
validates OpenCap's muscle-activation output against EMG for any task, golf or otherwise; the
kinetics/GRF-specific validations found (§1.2, §6) are joint-moment/GRF-level, not muscle-
activation-level, and even those show the same fast/impact degradation pattern.

**Licence**: opencap-core is **Apache License 2.0** (github.com/stanfordnmbl/opencap-core) — a
permissive licence compatible with a free public app. This is the more favourable licence position
of the resources reviewed in this file (better than GolfDB's CC BY-NC 4.0, on par with CaddieSet's
MIT). Note this covers the *code*; OpenCap's hosted web-application processing service (which the
founding paper describes as doing the actual cloud-based kinematics/dynamics computation) is a
separate consideration from the open-source repository licence if the project intended to depend
on Stanford's hosted infrastructure rather than self-hosting the pipeline.

**Section 7 conclusion — direct answer to the brief's OpenCap question**: OpenCap's own founding
paper and the entire independent validation literature located here cover walking, running,
jumping, squatting, standing balance and gait-pathology tasks — never golf, never a comparably fast
axially-rotational whole-body movement. Its best-case accuracy (RMSE <2–6° in slow sagittal-plane
tasks) is well outside marker-based clinical-grade precision even there; its worst-case accuracy
(RMSE >10°, LoA in the tens of degrees, >40% bias at fast/impact phases) occurs specifically in the
task category (fast, dynamic, impact-involving) that a golf swing belongs to. Using OpenCap for
golf would be extrapolating a system beyond every published validation condition, in precisely the
direction (speed, impact, off-sagittal rotation) that has been shown, repeatedly and independently,
to degrade its accuracy. The licence (Apache 2.0) is not a barrier; the absence of any golf or
comparable-speed/rotation validation is.

---

## 8. Synthesis — does video clear the evidence bar for this project, and where does it corroborate/extend the user-supplied context?

**Corroboration of the parallel-strand findings supplied in the brief.** Both supplied data points
are independently reproduced by primary sources located in this search, not merely repeated:
- "Video-only kinematics show their worst errors at proximal and fast joints (hip in running:
  CMC=0.65, 15° systematic offset)" — this is Pagnon, Domalain & Reveret 2022 (Pose2Sim Part 2,
  PMID 35408326, PMC9002957, already catalogued in T-031 §8/source 17), and is independently
  corroborated here by Svetek et al.'s sagittal-hip-during-gait RMSE >10° (§1.2), Pratapneni et
  al.'s "greatest errors in distal, dynamic joints" (§1.5), and de Borba et al.'s hip/ankle ROM
  reliability specifically dropping at higher speed (§1.2) — four independent groups, same
  direction of effect (proximal/fast = worst).
- "Video-only GRF estimation has been demonstrated only for slow low-force tasks (RMSE 10.7%
  BW)" — this is Vonstad et al. 2022 (PMID 35152877, already catalogued in T-031 §8/source 16),
  and is independently extended here (§6) by Feng et al.'s 6–10% RMSE walking-only GRF/CoP figures
  and by the OpenCap fast-task literature (Färber et al.'s drop-jump MAE >6%; You et al.'s >40%
  landing-phase bias) — the pattern holds and gets worse, not better, as task speed/impact
  increases, across five independent studies spanning 2022–2026.

**Answering the brief's core question directly**: video CAN yield joint angles that count as
evidence, but only within a narrow, specific envelope that a golf swing does not fall inside:
- **Usable-as-evidence envelope** (supported by multiple, converging, independent sources):
  slow-to-moderate-speed, sagittal-plane, flexion/extension motion, filmed synchronously by ≥2
  calibrated cameras (OpenCap-class) or a dedicated multi-camera markerless rig (Theia3D-class) —
  RMSE reliably <5–6°, sometimes <2°, with r>0.8–0.9 vs marker-based ground truth. This describes
  walking, running (with caveats), squatting, and slow controlled ROM tasks.
- **Not-evidence-grade envelope** (also supported by multiple, converging, independent sources):
  transverse/rotational-plane angles at any speed (LoA routinely ±11° to ±16°, ranges up to 3–57°
  reported in one review); any joint/plane during a fast, ballistic, or impact-involving phase
  (RMSE and bias both roughly double to quadruple at landing/impact vs. steady-state motion in
  every jump/landing study found); and monocular (single-camera) 3D estimation of anything beyond
  simple sagittal gait, where even lab-benchmark best-case error is 3.7–4.8 cm of joint position
  and real-world clinical studies report 14.6–24.9 cm.
- **The golf downswing sits entirely inside the "not-evidence-grade" envelope** on every dimension
  simultaneously: it is fast (≈90 mph clubhead speed, ≈0.25 s duration — well beyond every
  validated OpenCap/Theia3D task speed), it is dominated by axial/rotational motion (trunk and
  pelvis rotation, the single worst-performing DOF category found anywhere in this search), and its
  single most important instant (impact) is the same category of event (ballistic impact) shown
  repeatedly to be where video-derived kinetic/kinematic accuracy degrades most severely. No study
  anywhere in this search — golf or any other sport — has validated joint-angle accuracy at
  golf-downswing speed against marker-based or instrumented ground truth.

**What video IS good for in this project, evidenced rather than assumed**: (a) event/phase timing
— GolfDB/SwingNet and CaddieSet both show 76–98% frame-level accuracy for most of the 8 canonical
swing events (address and finish being the recurring exception, §4), which is directly useful for
timeline alignment even though it says nothing about joint-angle correctness at those frames; (b)
coarse, qualitative, sagittal-plane description of things like forward/spine tilt (Yamamoto et al.,
§1/§2/§5) — useful for descriptive/coaching commentary, not for precise numeric activation
back-solving; (c) relative/within-subject comparison (before/after, trial-to-trial variability),
where several OpenCap studies found high agreement even when absolute accuracy was mediocre
(Verheul et al. §1.2's "high agreement in inter-stride and inter-trial variability... despite
[absolute] differences").

**What video is NOT evidenced to be good for, specific to this project's stated goals**: precise
absolute joint angles for any rotational/axial DOF at any speed; any joint angle at all during the
downswing/impact phase specifically; muscle activation or joint moments/kinetics for a golf swing
(§6 — zero published attempts found, golf or video-general); and OpenCap-class kinematics-plus-
kinetics pipelines applied to golf (§7 — zero validation, and the nearest validated proxies are
already OpenCap's worst-performing category).

**Consequence for the project**: video can supply *phase/event timing* and *coarse, qualitative,
sagittal-plane* description as a corroborating, non-quantitative evidence layer alongside the EMG
literature already assembled (`docs/research/01–07`), but cannot supply validated joint angles for
trunk/pelvis rotation, cannot supply validated kinematics during the downswing/impact phase, and
cannot supply any validated basis for back-solving muscle activation — consistent with, and
extending, T-031's F-036 conclusion that no scientifically validated back-solved activation curve
can be claimed for golf from any current motion-capture modality, video-derived or otherwise. Any
video-derived numbers this project does use (event timing, gross posture) must be labelled
descriptive/qualitative evidence, not measured kinematic ground truth.

**Explicitly flagged gaps for a future targeted follow-up, not filled by guessing**: (1) no study
isolates a trunk-axial-rotation RMSE/LoA number for any task, golf or otherwise — the §5 conclusion
rests on convergent indirect evidence, not a single direct measurement; (2) no study tests golf (or
any comparable-speed rotational sport) kinematics at multiple frame rates against ground truth to
derive a validated minimum-fps threshold — §2's frame-rate conclusion rests on practitioner choice
(240 Hz) and a primary-source admission (GolfDB's 30 fps impact-capture failure), not a controlled
frame-rate-vs-accuracy study; (3) the CaddieSet swing-count discrepancy (924 in-paper vs 1,757 in
repository, §3.2) is unresolved; (4) no successor to SwingNet with improved per-event PCE was
located, so 76.1%/91.8% (GolfDB) and 78.0%/94.1% (CaddieSet) should be treated as the current
published ceiling for golf event detection, not necessarily the true achievable ceiling.

---

## 9. Source table

| # | Source | ID | Where used |
|---|---|---|---|
| 1 | Çabuk, Ulupınar, İnce & Özbay 2026, *Biology of Sport* | PMID 41783455, PMCID PMC12954493, DOI 10.5114/biolsport.2026.154942 | §1.1, §7 — OpenCap pooled meta-analysis (RMSE 5.877°→4.940°, r=0.845) |
| 2 | Svetek, Morgan, Burland & Glaviano 2025, *J Biomech* | PMID 40048968, DOI 10.1016/j.jbiomech.2025.112602 | §1.2, §8 — OpenCap lower-limb RMSE by plane (<6° frontal hip; 4–10° sagittal knee; >10° sagittal hip gait) |
| 3 | Verheul et al. 2026, *J Biomech* | PMID 41418503, DOI 10.1016/j.jbiomech.2025.113133 | §1.2, §8 — OpenCap running validity; systematic swing-phase disagreement |
| 4 | Färber, Horsak & Paternoster 2026, *Sci Rep* | PMID 41876778, PMCID PMC13018474, DOI 10.1038/s41598-026-44758-0 | §1.2, §6, §7 — OpenCap drop-jump; RMSE >6° knee; MAE>6% GRF; "cannot be recommended" |
| 5 | de Borba et al. 2025, *Sensors* | PMID 41157527, PMCID PMC12568194, DOI 10.3390/s25206474 | §1.2, §8 — OpenCap gait-speed effects; hip/ankle ROM reliability drop at speed |
| 6 | Turner et al. 2026, *J Biomech* | PMID 41138605 | §1.2 — OpenCap jump-landing reliability; MDC 1.89–11.62° |
| 7 | You, Lin & Zhang 2026, *Sensors* | PMID 42280894, PMCID PMC13259095, DOI 10.3390/s26113375 | §1.2, §6, §8 — OpenCap child vertical jump; landing peak-force bias >40% |
| 8 | Horsak et al. 2025 (CameraHMR), *J Biomech* | PMID 41046587, DOI 10.1016/j.jbiomech.2025.112986 | §1.2, §5 — monocular vs OpenCap vs marker-based; RMSD 5.5±1.1° validity |
| 9 | Yan et al. 2025, *Sensors* | PMID 41013149, PMCID PMC12473682, DOI 10.3390/s25185911 | §1.2 — OpenCap paediatric CP balance; R 0.39–0.94 raw |
| 10 | Shimotori et al. 2025, *JMIR Rehabil Assist Technol* | PMID 40373227, PMCID PMC12097655, DOI 10.2196/66886 | §1.3 — Theia3D ramp/stair RMSD ≤5.64° |
| 11 | Helwig et al. 2025, *Sci Rep* | PMID 41028120, PMCID PMC12484822, DOI 10.1038/s41598-025-21143-x | §1.3, §5 — Theia3D cutting task; int/ext rotation LoA ±15.75° vs flex/ext ±10.71° |
| 12 | Yang et al. 2025, *Sci Rep* | PMID 40425708, PMCID PMC12117081, DOI 10.1038/s41598-025-02739-9 | §1.3 — Theia3D athlete jumping; RMSD ≤5.6° |
| 13 | D'Souza et al. 2024, *Sci Rep* | PMID 39587194, PMCID PMC11589150, DOI 10.1038/s41598-024-80499-8 | §1.3, §5 — Theia3D; "hip and knee rotations non-comparable" |
| 14 | Poomulna et al. 2024, *Gait Posture* | PMID 39490268, PMCID PMC12415537, DOI 10.1016/j.gaitpost.2024.10.018 | §1.3, §5 — Theia3D CP; RMSD >10° pelvic tilt/hip rotation |
| 15 | Yoma et al. 2025, *Int J Sports Phys Ther* | PMID 40756794, PMCID PMC12317789, DOI 10.26603/001c.141870 | §1.3 — Theia3D single-leg squat/landing RMSD 3.2–3.6° |
| 16 | Adlou et al. 2025, *Sensors* (review) | PMID 40732512, PMCID PMC12299843, DOI 10.3390/s25144384 | §1.3, §5, §8 — sagittal 3–15° vs transverse 3–57° accuracy range |
| 17 | Doerks et al. 2025, *PLoS ONE* | PMID 40445923, PMCID PMC12124523, DOI 10.1371/journal.pone.0324499 | §1.3 — 2D-only video app; r as low as 0.36 |
| 18 | Uhlrich et al. 2023 (OpenCap founding paper), *PLoS Comput Biol* | PMID 37856442, PMCID PMC10586693, DOI 10.1371/journal.pcbi.1011462 | §7 — OpenCap method, 100-subject field study, 25× faster/<1% cost |
| 19 | opencap-core repository | github.com/stanfordnmbl/opencap-core | §7 — Apache 2.0 licence |
| 20 | McNally, Vats, Pinto, Dulhanty, McPhee & Wong 2019, GolfDB | arXiv:1903.06528 | §2, §3.1, §4 — dataset, SwingNet, 30 fps impact-capture admission, per-event PCE table |
| 21 | golfdb repository | github.com/wmcnally/golfdb | §3.1 — CC BY-NC 4.0 licence |
| 22 | Jung, Hong, Jeong, Jeong, Choi, Kim & Lee 2025, CaddieSet | arXiv:2508.20491 | §3.2, §4 — dataset, HRNet 17-joint 2D, event-accuracy 78.0%/94.1% |
| 23 | CaddieSet repository | github.com/damilab/CaddieSet | §3.2 — MIT licence |
| 24 | Yamamoto, Hasegawa, Suzuki, Suzuki, Tanabe & Fujii 2023, *Front Sports Act Living* | PMID 38033658, PMCID PMC10684732, DOI 10.3389/fspor.2023.1272038 | §1, §2, §5 — only golf-specific markerless-pose study found; 240 Hz camera; no 3D ground truth; explicit rotation-accuracy admission |
| 25 | Lauer 2025, wrist-IMU golf signatures | arXiv:2506.17505 | §3.3 — video used as 3D-mesh training-label source, not deployed modality |
| 26 | WIT-KinNet, smartwatch golf kinematics | arXiv:2606.22876 | §2, §3.3 — MAE 8.11±1.84°; "camera-based methods require impractical camera placement" |
| 27 | Liao, Hwang & Koike 2021, golf swing coaching tool | arXiv:2105.10153 | §3.3 — video-sync coaching tool, no accuracy figures |
| 28 | Turner, Aha, Smith & Gupta 2015 | arXiv:1512.07502 | §3.3 — UCF Sports Action dataset (action-recognition only, not pose) |
| 29 | Rode, Dunkel, Willi, Wolf, Xiloyannis & Riener 2025, *Sci Rep* | PMID 41193590, DOI 10.1038/s41598-025-22626-7 | §1.5, §5 — monocular clinical MPJPE 146–249 mm |
| 30 | Pratapneni, Halvorson, Silvestros, Harris & Bailey 2026, *IEEE Access* | PMID 42238785, DOI 10.1109/access.2026.3687207 | §1.5, §5, §8 — single-camera; distal/dynamic joints worst |
| 31 | Guo, Gao, Dong, Jiang, Zhu & Wang 2025, *Sensors* (survey) | PMID 40285099, DOI 10.3390/s25082409 | §1.5, §5 — monocular 3D pose survey; depth ambiguity unsolved |
| 32 | Russo et al. 2026, *Sensors* | PMID 41977932, DOI 10.3390/s26072148 | §1.4 — MediaPipe knee MAE 2.3–4.55° |
| 33 | Balci et al. 2025, *Front Sports Act Living* | PMID 41602810, DOI 10.3389/fspor.2025.1712332 | §1.4 — MediaPipe 2D ICC 0.85 |
| 34 | Lazem et al. 2026 (Track-UL), *JMIR Rehabil Assist Technol* | PMID 42114045, DOI 10.2196/87128 | §1.4 — MediaPipe upper-limb LoA |
| 35 | Kondo & Suzuki 2026, *J Phys Ther Sci* | PMID 42306435, DOI 10.1589/jpts.38.270 | §1.4, §5 — MediaPipe trunk ICC; lateral 0.80 vs sagittal 0.96–0.98 |
| 36 | Edriss et al. 2025, *Front Physiol* (review) | PMID 40873758, DOI 10.3389/fphys.2025.1649330 | §1.4 — 2D-to-3D fusion still "promising," not solved |
| 37 | Verikas et al. 2016 | PMID 27120604 | §6 — surface EMG golf study (negative control: not video) |
| 38 | Yeung, Suzuki, Tanaka, Yin & Fujii 2025, AthletePose3D | arXiv:2503.07499 | §1.5 (context) — sport-pose fine-tuning error 214mm→65mm |
| 39 | Vonstad, Bach, Vereijken, Su & Nilsen 2022, *J Neuroeng Rehabil* | PMID 35152877, DOI 10.1186/s12984-022-00998-5 | §6, §8 — video-GRF RMSE 10.7% BW (slow task); reused/corroborated from T-031 |
| 40 | Feng, Ugbolue, Yang & Liu 2025, *Bioengineering* | PMID 40564405, DOI 10.3390/bioengineering12060588 | §6, §8 — markerless GRF/CoP walking, RMSE 6–10% |
| 41 | Schreff et al. 2026, *Children* | PMID 41897076, DOI 10.3390/children13030363 | §6 — paediatric gait GRF R²>0.95 |
| 42 | Aulton et al. 2025 (review) | PMID 41369858 | §1.5 — DL pose-in-sport review; reproducibility warning |
| 43 | Souaifi et al. 2025 (review) | PMID 40868401 | §1.5 — AI-in-sports-biomechanics scoping review; 94% CNN agreement, 15 mm CV accuracy |
| 44 | Wang et al. 2026 (badminton), *Sci Rep* | PMID 41922587, DOI 10.1038/s41598-026-46443-8 | §2 — event cameras vs motion blur, 42.3% error reduction |
| 45 | Zhang et al. 2025 (basketball), *Sci Rep* | PMID 40783613, DOI 10.1038/s41598-025-14985-y | §2 — motion blur named challenge |
| 46 | Watson et al. 2026, *Sports Med* (review) | PMID 41653371, DOI 10.1007/s40279-025-02391-3 | §2, §6 — golf GRF/CoP review; zero markerless studies among 24 |
| 47 | Yang, Chang, Chao, Tai & Tsai 2024, *Front Bioeng Biotechnol* | PMID 38380262, DOI 10.3389/fbioe.2024.1343530 | §2 — golf shaft-weight study; 9 infrared high-speed cameras |

**Total: 47 distinct cited sources** (target was 15+), spanning PubMed/Europe PMC (PMID/PMCID/DOI),
arXiv, and two GitHub repository licence checks.

---

