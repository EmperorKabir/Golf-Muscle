# T-032 — Golf Swing Kinematics (Joint Angle Time Series for Animation)

Research basis for driving the 3D model's animation directly from measured kinematics, since a
parallel research strand (T-031, `docs/research/09-inverse-activation-estimation.md`, F-036)
established that muscle activation cannot be reliably back-solved from motion alone. This document
is the kinematic counterpart: joint angles, angular velocities and timing needed to pose/animate the
skeleton through a full swing, for a right-handed golfer, iron shot where the source specifies.

**Session constraints:** no sub-agents (single sequential pass); WebSearch unavailable (exhausted),
all retrieval via WebFetch against the Europe PMC REST API (`https://www.ebi.ac.uk/europepmc/webservices/rest/search`)
and PMC full text (`https://pmc.ncbi.nlm.nih.gov/articles/PMCxxxxxxx/`), plus PubMed HTML search.
Every numeric value is cited to its source. Values are given as reported — where a source uses a
sign convention (e.g. negative = away from target), the convention is stated rather than silently
normalised.

---

## Status: COMPLETE (single-session pass, no sub-agents, WebFetch-only per session constraints). See
§14 for a coverage summary against the 12 requested items, and the numbered "flagged"/"gap" notes
throughout for items needing a follow-up pass.

---

## 1. Pelvis and thorax (upper torso) rotation — angle and velocity data

### 1.1 Severin AC et al. (2022), "Three-dimensional kinematics in healthy older adult males during
golf swings," *Sports Biomechanics*. PMC7044058 / doi:10.1080/14763141.2019.1649452. n=17 healthy
older male golfers (1.77±0.07 m, 91.3±11.1 kg, 62.2±8.8 years); driver vs six-iron compared.
**Caveat: older-adult sample (mean 62 y), not the young-elite population most other sources use —
values likely understate range of motion/velocity versus a younger competitive golfer.**

Trunk = sagittal-plane forward flexion of upper torso; Pelvis/X-factor = transverse plane;
sign convention as reported by the source (not renormalised).

| Event | Segment/measure | Driver | 6-iron |
|---|---|---|---|
| Top of backswing | Trunk (sagittal) | −28.3° ± 5.6° | −35.6° ± 6.6° |
| Top of backswing | X-factor (transverse, pelvis-thorax separation) | −33.0° ± 11.0° | −37.3° ± 8.3° |
| Top of backswing | Pelvis (sagittal) | −14.2° ± 3.8° | −15.3° ± 4.3° |
| Top of backswing | Lead hip (sagittal) | 17.7° ± 10.5° | 19.1° ± 11.1° |
| Top of backswing | Trail hip (sagittal) | 27.8° ± 9.7° | 26.6° ± 7.7° |
| Top of backswing | Lead knee (sagittal) | 45.2° ± 10.0° | 48.6° ± 8.4° |
| Ball impact | Trunk (sagittal) | 30.4° ± 5.9° | 40.9° ± 5.8° (driver 10.5° less flexed) |
| Ball impact | X-factor (transverse) | −14.9° ± 9.5° | −18.1° ± 8.9° (driver 3.2° less) |
| Ball impact | Pelvis (transverse) | 20.8° ± 10.6° | 15.6° ± 11.1° |
| Ball impact | Trail hip (sagittal) | 7.1° ± 8.4° | 12.4° ± 8.4° |
| Ball impact | Lead hip (sagittal) | 11.7° ± 7.5° | 13.4° ± 7.6° |
| Ball impact | Lead knee (sagittal) | 23.5° ± 9.2° | 23.7° ± 8.7° |
| End of swing (finish) | Trunk (sagittal) | −4.0° ± 7.5° | −9.1° ± 9.2° |
| End of swing | Pelvis (transverse) | 88.8° ± 16.1° | 82.4° ± 15.5° |
| End of swing | X-factor (transverse) | 29.7° ± 10.6° | 33.4° ± 7.9° |

X-factor stretch (max separation reached in transition, beyond top-of-backswing X-factor):
driver 35.8° ± 11.6°, 6-iron 37.9° ± 8.1° (not significantly different between clubs).

Peak angular velocities (°/s):
| Plane | Segment | Phase | Driver | 6-iron |
|---|---|---|---|---|
| Sagittal | Trunk | follow-through | 164.9 ± 41.6 | 138.9 ± 30.4 |
| Sagittal | Trail ankle | downswing | −60.5 ± 25.2 | −30.3 ± 17.6 |
| Sagittal | Trail hip | downswing | −175.6 ± 35.4 | −148.8 ± 38.5 |
| Sagittal | Lead hip | downswing | −126.6 ± 54.0 | −154.7 ± 51.1 |
| Frontal | Trunk | follow-through | 223.4 ± 60.5 | 254.2 ± 74.8 |
| Frontal | Pelvis | downswing | 113.3 ± 32.5 | 136.0 ± 38.8 |
| Frontal | Trail hip | downswing | −132.0 ± 42.9 | −163.5 ± 49.5 |
| Transverse | X-factor | follow-through | 155.2 ± 55.9 | 133.5 ± 37.6 |
| Transverse | Pelvis | downswing | 315.0 ± 52.5 | 283.2 ± 54.1 |
| Transverse | Lead knee | downswing | 152.3 ± 28.1 | 121.9 ± 42.9 |

Performance context: club head speed driver 39.4 ± 4.4 m/s vs 6-iron 33.8 ± 4.4 m/s; ball speed
driver 56.1 ± 7.3 m/s vs 6-iron 45.1 ± 6.0 m/s.

### 1.2 Zhou JY et al. (2022), "The Swing Performance Index: developing a single-score index of golf
swing rotational biomechanics quantified with 3D kinematics," *Frontiers in Sports and Active
Living*. PMC9816382 / doi:10.3389/fspor.2022.986281. Professional golfers, peak rotational
velocities (°/s):

| Segment | Phase | Mean ± SD | CV |
|---|---|---|---|
| Upper torso | downswing | 551.7 ± 47.6 | 0.086 |
| Upper torso | impact | 458.5 ± 73.0 | 0.159 |
| Upper torso | follow-through | 929.2 ± 185.1 | 0.199 |
| Pelvis | downswing | 415.2 ± 32.9 | 0.079 |
| Pelvis | impact | 288.8 ± 70.9 | 0.245 |
| Pelvis | follow-through | 309.8 ± 42.1 | 0.136 |

X-prime (upper-torso-minus-pelvis relative rotational velocity), °/s: downswing −183.4 ± 41.4 (CV
−0.23); impact −170.3 ± 63.0 (CV −0.37); follow-through −729.4 ± 160.8 (CV −0.22). Swing
Performance Index (composite, not an angle): professionals 100 ± 10 vs amateurs 82 ± 4 (SMD 2.12).
**Note: this paper reports peak velocities by phase, not absolute angular displacement in degrees
or ms/%-swing timing for those peaks — a gap for animation purposes.**

### 1.3 Grathwohl & Sillevis (2024), case report, *American Journal of Case Reports*. PMC11642117 /
doi:10.12659/AJCR.946077. K-Vest sensor swing analysis, single subject, pre/post a training
intervention (both data points usable as independent within-swing snapshots):

| Measure | Pre-intervention | Post-intervention |
|---|---|---|
| Pelvis rotation at address | 7° | −1° |
| Trunk rotation at address | 6° | 12° |
| Pelvis bend (posture) at address | 24° | 21° |
| Trunk bend (posture) at address | 26° | 35° |
| Pelvis rotation at top | −43° | −40° |
| Pelvis rotation at impact | 12° | 18° |
| Trunk rotation at top | −83° | −82° |
| Trunk rotation at impact | 7° | 7° |

Implied X-factor at top (trunk − pelvis): pre −83−(−43)=−40°; post −82−(−40)=−42° — consistent in
magnitude with the Severin driver value (−33.0°) and 6-iron value (−37.3°) above, and with
Bourgain's pooled 28–57° range depending on measurement method (§4 below).

Physical-examination mobility (not swing kinematics, but useful ROM context — measured supine/seated,
not during the swing): seated trunk rotation right 48°→65° pre→post, left 60°→75°; shoulder internal
rotation (supine) right 58°→74°, left 46°→57°; shoulder external rotation (supine) right 76°→85°,
left 80°→85°.

---

## 2. Kinematic sequence (proximal-to-distal timing)

- Bourgain et al. 2022 (systematic review, §above) confirms the proximal-to-distal kinematic
  sequence concept (pelvis peaks first, then thorax, then arm, then club) is the standard model
  following Cheetham et al. and Tinmark et al., but flags it as **methodologically fragile**: the
  computed sequence depends heavily on whether angular velocity is derived from Euler-parameter time
  derivatives or from time-differentiated rotation matrices, and switching method "strongly modifies
  the estimated kinematic sequence" in the same dataset. Neal et al.'s reported inter-method timing
  differences (4–56 ms) are flagged as being close to or below measurement accuracy.
  **Consequence for animation: the qualitative order (pelvis → thorax → lead arm → club) is
  well-supported; exact millisecond gaps between segment peaks are method-dependent and should not
  be hard-coded as a single authoritative figure.**
- Horan et al. (cited in Bourgain 2022) additionally propose head as leading the sequence: head,
  pelvis, torso, with a measured rotational speed of **≈210 ± 56°/s** for the head-segment measure
  used in that sequence (exact segment/axis definition not recoverable from the secondary citation —
  flagged as needing primary-source confirmation if used quantitatively).
- Downswing total duration (Bourgain 2022, pooled across skill levels): **≈0.3 s**, broken out by
  skill/club: male recreational driver 0.25 ± 0.02 s; male highly skilled driver 0.31 ± 0.04 s; male
  professional driver 0.31 ± 0.04 s; female driver 0.39 ± 0.08 s. (Consistent with T-011a's existing
  phase-timing file, `docs/research/01-phase-taxonomy-and-timing.md`.)

---

## 3. Torso, shoulder, elbow and wrist range-of-motion — Bourgain 2022 systematic-review pooled table

These are **amplitude/range values** (max-to-min excursion through the swing, not fixed values at a
single event) pooled by Bourgain et al. 2022 from the reviewed literature (their Tables 6–10),
lead/trail = golfer's lead/trail side for a right-handed golfer:

| Segment/joint | Measure | Value |
|---|---|---|
| Torso | Axial rotation (amplitude) | 129° |
| Torso | Lateral bending (amplitude) | 28° |
| Torso | Flexion/extension (amplitude) | 33° |
| Lead shoulder | Clavicle protraction | 27° |
| Lead shoulder | Clavicle elevation | 25° |
| Lead shoulder | Shoulder elevation | 100° |
| Lead shoulder | Humeral flexion | 42° |
| Lead shoulder | Humeral axial rotation | 64° |
| Trail shoulder | Clavicle protraction | 38° |
| Trail shoulder | Clavicle elevation | 6° |
| Trail shoulder | Shoulder elevation | 13° |
| Trail shoulder | Humeral flexion | 34° |
| Trail shoulder | Humeral axial rotation | 125° |
| Lead elbow | Flexion (amplitude) | 26° |
| Lead elbow | Pronosupination (amplitude) | 153° |
| Trail elbow | Flexion (amplitude) | 95° |
| Trail elbow | Pronosupination (amplitude) | 71° |
| Lead wrist | Flexion (amplitude) | 38° |
| Lead wrist | Radial/ulnar deviation (amplitude) | 90° |
| Trail wrist | Flexion (amplitude) | 86° |
| Trail wrist | Radial/ulnar deviation (amplitude) | 28° |
| Lead knee | Flexion/extension (amplitude) | 15° |
| Trail knee | Flexion/extension (amplitude) | 8° |
| Lead knee | Internal/external rotation (amplitude) | 18° |
| Trail knee | Internal/external rotation (amplitude) | 25° |
| Lead knee | A-P translation | 5 mm |
| Trail knee | A-P translation | 4 mm |
| Lead hip | Internal/external rotation (amplitude) | 50° |
| Trail hip | Internal/external rotation (amplitude) | 40° |
| Lead hip | Adduction/abduction (amplitude) | 45° |
| Trail hip | Adduction/abduction (amplitude) | 40° |
| Lead hip | Flexion/extension (amplitude) | 30° |
| Trail hip | Flexion/extension (amplitude) | 45° |

Knee flexion time-course (lead side, Murakami et al., as pooled in Bourgain 2022): address 18±12°,
early backswing 22°, late backswing 26°, top of backswing 33±8°, impact 25°, end of follow-through
16±9°. Trail side: address 17±9°, top of backswing 24±8°, impact 22°. Lead knee internal/external
rotation: address 2±6°, top of backswing −7±7°, end of follow-through 10±5°.

X-factor (torso-pelvis separation), method-dependent — **do not average across methods**:
- Torso-pelvis method, recreational golfers: 28 ± 13° (horizontal/swing-plane projections).
- Shoulder-pelvis method, recreational golfers: 57.1 ± 11.2° (horizontal), 57.7 ± 10.5° (swing
  plane), 54.4 ± 10.3° (3D).
- Shoulder-pelvis method, professional/elite reference group (8 professionals + 2 elite amateurs):
  48°.

Clubhead speed at impact (context, not a joint angle): men's driver recreational 33–53 m/s, highly
skilled amateur 45.4 ± 3.6 m/s, professional 50.1 ± 2.1 m/s; men's iron recreational 33.8 ± 2.5 m/s,
highly skilled amateur 37.65 ± 1.04 m/s; women's driver 37.7 ± 3.8 m/s, women's iron 32 ± 1 m/s.

Spine-loading note: "for professional golfers, lumbar and lead-hip rotation were equally
distributed," whereas lower-skilled golfers show a different distribution; "a lack of mobility for
the lead hip has been linked to higher use of the lumbar spine" (Bourgain 2022) — i.e. restricted
lead-hip internal rotation is compensated by extra lumbar axial rotation, which is clinically
relevant given how little the lumbar spine is built to rotate (§6 below).

---

## 4. Lead/trail shoulder, elbow, wrist — event-resolved data (Wheare et al. 2021)

Wheare MJ et al. (2021), "Reliability and Validity of the Polhemus Liberty System for Upper Body
Segment and Joint Angular Kinematics of Elite Golfers," *Sensors* 21(13):4330. PMC8271493 /
doi:10.3390/s21134330. n=15 elite amateur/professional golfers, electromagnetic tracking
(Polhemus Liberty), two trial conditions (ranges given below span the two conditions' means).

**Lead (left) shoulder:**
| Axis | Address | Top of backswing | Impact |
|---|---|---|---|
| Medial-lateral (elevation) | −64.6° (SD 4.4) to −64.0° (SD 3.5) | 5.3° (SD 9.6) to 6.5° (SD 9.8) | −51.1° (SD 8.2) to −49.6° (SD 7.4) |
| Anterior-posterior (abduction/adduction) | 52.0° (SD 8.4) to 54.1° (SD 7.2) | 41.7° (SD 6.1) to 42.4° (SD 5.9) | 54.9° (SD 7.7) to 55.6° (SD 6.7) |

**Lead (left) wrist:**
| Axis | Address | Top of backswing | Impact |
|---|---|---|---|
| Medial-lateral (flexion/extension) | −20.5° (SD 14.7) to −22.2° (SD 10.3) | −12.0° (SD 18.8) to −10.4° (SD 20.7) | 1.0° (SD 14.6) to 1.4° (SD 12.6) |
| Anterior-posterior (radial/ulnar deviation) | 33.3° (SD 6.6) to 31.7° (SD 7.8) | −5.1° (SD 13.9) to −5.7° (SD 20.4) | 44.2° (SD 7.0) to 42.6° (SD 6.8) |

**Trail (right) wrist:**
| Axis | Address | Top of backswing | Impact |
|---|---|---|---|
| Medial-lateral | 6.3° (SD 9.6) to 5.6° (SD 10.1) | −50.0° (SD 10.1) to −49.0° (SD 10.7) | 0.3° (SD 18.0) to −1.3° (SD 16.7) |
| Anterior-posterior | 32.1° (SD 6.6) to 31.7° (SD 6.2) | 29.3° (SD 17.2) to 28.7° (SD 19.5) | 40.2° (SD 11.8) to 41.1° (SD 7.9) |

**Gap flagged:** the source's abstract/extractable tables cover lead shoulder, lead wrist and trail
wrist; elbow-specific angle tables and the trail shoulder table were not recoverable from the
fetched text — may require the full PDF's figures/tables beyond what WebFetch's HTML extraction
surfaced. Cross-reference against §3's Bourgain pooled elbow/trail-shoulder amplitude values instead.

---

## 5. Lumbar spine — sagittal/frontal kinematics and loads during the downswing

Chen et al. (2024), "Does Overhead Squat Performance Affect the Swing Kinematics and Lumbar Spine
Loads during the Golf Downswing?" *Sensors* 24(5). PMC10893031. Two groups by score (low-scoring
"LS" = better players, high-scoring "HS" = worse players), values are angular displacement/peak
during the downswing:

| Measure | Low-scoring (better) | High-scoring (worse) | Sig. |
|---|---|---|---|
| Lumbar flexion angle at impact (sagittal) | −21.37° ± 6.39° | −26.20° ± 5.90° | — |
| Lumbar extension angular displacement | 17.72° ± 5.94° | 24.36° ± 7.11° | p=0.031 |
| Lumbar peak extension angular velocity | 119.52 ± 59.23 °/s | 40.51 ± 26.79 °/s | p<0.001 |
| Lumbar peak flexion angular velocity | −269.34 ± 181.03 °/s | −288.95 ± 162.68 °/s | n.s. |
| Lumbar right-side-bend angle at impact (frontal) | 21.07° ± 0.48° | 20.93° ± 0.70° | n.s. |
| Lumbar bending angular displacement | 34.89° ± 5.95° | 31.21° ± 7.28° | n.s. |

Lumbar joint peak shear force: L4-L5 LS 387.19 ± 89.16 N vs HS 299.54 ± 37.30 N (p=0.010); L5-S1 LS
525.19 ± 86.69 N vs HS 407.90 ± 59.06 N (p=0.002); L1-L2/L2-L3/L3-L4 shear reported but n.s. between
groups. Peak compressive force across all lumbar levels: range 3018.92–3921.69 N, n.s. between
groups. (Force data included for completeness though outside the animation scope — relevant if this
project ever links kinematics to injury-risk loading.)

**Cross-reference note:** the ~21° lumbar right-side-bend at impact here is broadly consistent with
general observations of pronounced lateral trunk flexion at impact in golf swing literature (see §8
posture below), though this source isolates the lumbar segment specifically rather than whole-trunk
side bend.

---

## 6. Hip, knee and ankle — event/range data during the downswing (lead leg)

Lin et al. (2023), "Lower Limb Biomechanics during the Golf Downswing in Individuals with and
without a History of Knee Joint Injury," *Bioengineering* 10(2). PMC10215287. Values are peak
angles reached during the downswing phase (not separately broken out by address/top/impact in the
extractable table); KIH+ = history of knee injury, KIH− = no injury history; lead leg only:

| Joint | Measure | KIH+ | KIH− |
|---|---|---|---|
| Hip | Flexion | 31.15° ± 15.29° | 17.44° ± 8.52° |
| Hip | Extension | 1.84° ± 10.79° | −5.78° ± 7.54° |
| Hip | Adduction | 8.29° ± 5.88° | 7.40° ± 3.65° |
| Hip | Abduction | −31.94° ± 10.58° | −29.54° ± 6.16° |
| Hip | Internal rotation | 43.98° ± 17.31° | 42.11° ± 10.68° |
| Hip | External rotation | −27.07° ± 11.92° | −29.99° ± 10.10° |
| Knee | Flexion | 42.27° ± 11.12° | 37.06° ± 7.44° |
| Knee | Extension | 10.29° ± 11.47° | 5.61° ± 5.50° |
| Knee | Internal rotation | −20.26° ± 9.56° | −22.32° ± 8.35° |
| Knee | External rotation | −37.92° ± 8.39° | −41.27° ± 6.70° |
| Ankle | Plantarflexion | 20.59° ± 5.00° | 17.96° ± 2.96° |
| Ankle | Dorsiflexion | −3.28° ± 9.54° | −4.52° ± 6.26° |
| Ankle | Adduction | 19.50° ± 4.72° | 20.82° ± 3.16° |
| Ankle | Abduction | 10.48° ± 3.64° | 15.21° ± 3.12° |

**Note:** lead-leg hip internal rotation of ~42–44° here is notably larger than Bourgain's pooled
amplitude figure of 50° total IR/ER range (§3) — broadly consistent (this is a peak value within
that range, not a contradiction) but flags that individual-study hip-rotation numbers vary
considerably by measurement convention; treat as indicative magnitude, not a single ground truth.

---

## 7. Address posture and spinal loading — Edwards, Dickin & Wang (2020)

Edwards N, Dickin C, Wang H (2020), "Low back pain and golf: A review of biomechanical risk
factors," *Sports Medicine and Health Science* 2(1). PMC9219256 / doi:10.1016/j.smhs.2020.03.002.

- **"In an optimal address position, golfers have 45° of trunk flexion and a neutral spine
  profile."** This is the clearest single figure found for forward spine/trunk tilt at address —
  **directly usable for the model's address pose**, though the review does not specify whether this
  is measured from vertical or some other reference, or break it into thoracic vs lumbar
  contribution — flagged for cross-check if a second source becomes available.
- Effect of altered lumbar posture on rotation ROM (from a cited biomechanical experiment):
  lumbar hyperextension reduced trunk rotation ROM by 4.2% but increased pelvis ROM by 4%; 22.5° of
  lumbar flexion reduced trunk rotation ROM by 5% and pelvis ROM by 17%. (Relevant to rigging: the
  model's spine curvature at address will materially affect how much rotation ROM "looks right" at
  the top of the backswing.)
- Spinal loading (not a kinematic angle, included for the injury-mechanism context this project may
  want later): L4-L5 compressive force **6.5 to 8+ × body weight immediately after impact**; in golfers
  with low back pain, compressive and lateral shear forces are 26.3% and 75.5% larger respectively
  than in healthy golfers performing the same bending/lifting tasks (cited from a non-golf-specific
  comparison task within the same review).
- Coupled-motion description (qualitative, no degree figures given): "during trunk rotation, the
  L2–L4 vertebrae bend away from the direction of rotation, while L4–S1 bend toward the direction of
  rotation," producing the net trunk motion — i.e. the lumbar spine's contribution to axial rotation
  is not a simple single-axis twist even within its small total ROM (§9 below).

---

## 8. Lateral side bend at impact — consolidated

Multiple independent figures converge on pronounced lateral trunk flexion (side bend) toward the
lead side by impact, though exact magnitude varies by what's measured:
- Chen et al. 2024 (§5): lumbar-segment-only right-side-bend at impact ≈ 21° (LS 21.07°, HS 20.93°;
  n.s. between groups) — this isolates the lumbar contribution specifically.
- Whole-trunk lateral bending amplitude through the swing (Bourgain 2022 pooled, §3): 28° (this is a
  range/amplitude figure, not an impact-specific value, so not directly comparable to the Chen
  figure above without knowing the amplitude's start point).
- No source found gives a single agreed "degrees of side bend at impact from a vertical reference,"
  which is the form most directly usable for a rig target-pose. The Chen 21° lumbar figure is the
  most defensible single number if the model needs one, but should be read as lumbar-only, not
  whole-trunk.

---

## 9. Lumbar axial rotation — the anatomical limit (rigging constraint)

**Figure: total lumbar spine axial rotation capacity ≈ 5–9° (about 1–2° per motion segment).**

Source: White AA, Panjabi MM (1990), *Clinical Biomechanics of the Spine*, 2nd ed., J.B. Lippincott,
p.107 — the standard reference cadaveric/biomechanical segmental-motion table, retrieved via the
"Lumbar vertebrae" Wikipedia article's citation of that table (primary textbook itself not directly
fetchable via WebFetch in this session — **flag: secondary retrieval of a primary print source,
treat the exact per-segment breakdown as indicative rather than independently verified against the
book itself**). Per-segment axial rotation ROM given:

| Segment | Axial rotation ROM |
|---|---|
| L1–L2 | 2° |
| L2–L3 | 2° |
| L3–L4 | 2° |
| L4–L5 | 2° |
| L5–S1 | 1° |
| **Total lumbar (L1–S1)** | **≈9° to one side (sum of segments), commonly rounded to "5–7°" or "about 5°" in secondary golf/spine literature** |

**Why this matters for rigging:** the whole-torso axial rotation amplitude through a golf swing is
~129° (Bourgain 2022, §3), and X-factor (shoulder-pelvis separation) alone reaches 48–57° (§3). If
the lumbar spine can only contribute a genuine ~5–9° of true axial twist, the overwhelming majority
of "trunk rotation" visible in a golf swing must be produced by: (a) the thoracic spine (which has
substantially greater per-segment axial rotation capacity — general spine biomechanics places
thoracic axial rotation at several degrees per segment, greater than lumbar, though this session did
not recover a directly citable golf-specific thoracic total figure — **flagged as an unverified
gap**), (b) hip axial rotation (lead hip IR/ER amplitude ~50°, trail ~40°, §3/§6), and (c) pelvis
rotation itself relative to the ground/feet. **Practical consequence for the rig:** the spine chain
in the 3D model should be built so that only a small fraction (roughly 5–10°, i.e. under 10% of the
visible "trunk turn") of the total apparent torso-relative-to-pelvis rotation is allocated to lumbar
vertebral segments; the larger share belongs to thoracic segments, hip rotation, and pelvis-vs-foot
rotation. Encoding the full ~50–90° of apparent trunk-pelvis separation as pure lumbar rotation would
be anatomically impossible and should be treated as a rigging bug if it occurs.
- Cross-reference: Bourgain 2022 (§3) independently reports, from the golf literature itself, "for
  professional golfers, lumbar and lead-hip rotation were equally distributed" and "a lack of
  mobility for the lead hip has been linked to higher use of the lumbar spine" — i.e. even the golf
  biomechanics literature treats extra lumbar rotation (beyond its small anatomical budget) as a
  compensation pattern associated with restricted hip mobility, not a normal/desirable source of
  trunk turn. This is indirect corroboration of the White & Panjabi constraint from a completely
  different literature (golf injury-mechanism papers), independent of the Wikipedia/textbook route.

---

## 10. Head position and stability

**Largely unresolved — the weakest-covered item in this document.** Searches for cranial head
lateral sway/displacement (cm/mm) and head rotation/tilt through the swing returned no usable
numeric results in this session (one promising-looking hit was a false positive: a hip-arthroplasty
study measuring femoral *head* — the ball-and-socket hip joint component — translation in
millimetres, not the golfer's cranial head).

What is available:
- Bourgain 2022 (§2, citing Horan et al.) treats the head as a distinct segment in an extended
  kinematic sequence (head → pelvis → torso), giving it a rotational speed of **≈210 ± 56°/s** — but
  the exact axis/definition of this "head rotation" (about the neck? about the spine's long axis
  measured at the head?) could not be confirmed from the secondary citation. Treat this number as
  provisional.
- No source quantified head TRANSLATION (the "keep your head still/behind the ball" coaching cue,
  which in reality permits some lateral and vertical drift) in this session.
- **Recommendation for the model:** absent quantified data, animate the head as approximately
  following the top of the thoracic spine chain (i.e. driven kinematically by the neck/upper-torso
  rig rather than an independently-authored head trajectory), and treat any specific "head stays
  still" claim as a coaching simplification rather than a validated kinematic constraint. This is a
  genuine research gap, not just an unsummarised one — flag for a follow-up pass if head realism
  becomes a priority (e.g. searching directly for "golf swing head kinematics C7" or a specific
  named marker/segment study, which this session's search terms did not surface).

---

## 11. Publicly available 3D motion capture datasets of golf swings

**Direct answer: no openly licensed 3D marker-based/joint-angle motion capture dataset of golf
swings was found. One relevant 2D video dataset exists (GolfDB) but it is not 3D kinematic data and
is licensed non-commercially.**

- **GolfDB** (McNally WJ et al., "GolfDB: A Video Database for Golf Swing Sequencing," CVPR
  Workshops 2019). Confirmed via direct fetch of the repository (github.com/wmcnally/golfdb):
  contains trimmed **2D video clips** (160×160 px) of golf swings sourced from YouTube, with
  annotations for **8 swing events** (address, toe-up, mid-backswing, top, mid-downswing, impact,
  mid-follow-through, finish) — built for the task of *swing event/phase detection in video*, not for
  3D joint-angle or marker-trajectory data. **Licence: Creative Commons Attribution-NonCommercial 4.0
  International** (code); preprocessed clips distributed via a Google Drive link; original clips
  reconstructable from listed YouTube URLs. Baseline SwingNet model: 71.5% event-detection accuracy.
  **Not directly usable to animate 3D joint angles** without running a separate 2D-to-3D pose-lifting
  model on the footage, and even then accuracy/validation for golf specifically is not established —
  and the NC licence would need checking against this project's eventual commercial status before any
  derived data is used.
- **CMU Graphics Lab Motion Capture Database** (mocap.cs.cmu.edu) — the best-known general-purpose
  open motion-capture database (CC-style free-for-any-purpose licence), covers locomotion, sports,
  dance and interaction categories. **Could not be checked in this session**: the site's TLS
  certificate failed validation on every WebFetch attempt (`unable to verify the first certificate`)
  on both the HTTPS and HTTP subject-listing pages. Whether it contains any golf-swing trials is
  **unconfirmed** — flagged as a concrete follow-up action (try again from a different network path,
  or check the database's published subject/category index via a mirror such as
  https://github.com/CMU-Perceptual-Computing-Lab or a research paper's supplementary materials that
  cites specific CMU-mocap subject/trial numbers for golf, if one exists).
- No golf-swing-specific dataset was found on Figshare, Zenodo, or as a "data descriptor" paper
  within Europe PMC's index (searches for "golf swing motion capture dataset," "golf swing database,"
  and "golf swing 3D pose SMPL benchmark" returned no matching releases).
- Every numeric kinematic source used in this document (Severin 2022, Zhou 2022, Wheare 2021,
  Grathwohl 2024, Chen 2024, Lin 2023) is drawn from a **published paper's summary statistics**
  (means/SDs at named events), not from a redistributable raw trajectory dataset — none of these
  papers' underlying marker data appears to be openly deposited alongside the article.
- **Bottom line for the project:** there is no drop-in open 3D mocap dataset to drive the animation.
  The practical path is what this document already provides — reconstructing a representative pose
  timeline from the published per-event/per-phase angle tables above (§1, §3, §4, §5, §6), keyframed
  at the swing events these papers already use (address, top of backswing, impact, finish), rather
  than interpolating a continuous curve from raw open motion-capture frames.

---

## 12. Anthropometry — does 189 cm stature with long femurs change the joint angles?

**No golf-specific study relating golfer height/limb-segment length to swing joint angles was found
in this session** (multiple search phrasings on Europe PMC and PubMed returned zero or irrelevant
results). This is a genuine gap, not a search-phrasing failure alone — the golf biomechanics
literature indexed here overwhelmingly reports pooled means across mixed-height samples without
stratifying or regressing by stature.

What can be stated with reasonable confidence from the data already gathered, as a **reasoned
inference, not a directly sourced golf-specific finding**:
- Every joint-angle figure in this document (§1, §3, §4, §5, §6) is an **angle**, which is a
  dimensionless, scale-independent quantity by construction — two golfers of different heights
  swinging with geometrically similar technique would in principle show the same joint angles at
  each event even though their linear measures (arm length, swing radius, clubhead path length,
  clubhead linear speed for a given angular speed) differ. This is a standard property of angular
  kinematics in biomechanics (angles don't carry a length unit), not something this session found a
  directly-citable golf-specific source stating outright — flagged accordingly.
  - **Consequence:** the joint ANGLE values in this document (§1, §3–§6) should be usable directly
    for a 189 cm golfer without rescaling.
  - **What would need to scale instead:** segment lengths in the rig itself (already handled by the
    189 cm/long-femur body model, T-014, independent of this document), and any LINEAR quantity
    derived from an angle (e.g. hand path radius, clubhead speed for a given angular velocity) —
    these scale with limb length even when the angle profile is unchanged.
- One partially relevant data point: Severin et al. 2022's sample (§1.1) has mean height 1.77 ± 0.07
  m — noticeably shorter than 189 cm, and the sample is also older (mean 62.2 y) — so if there is any
  stature-linked deviation from that paper's numbers, it would not be visible from within that single
  dataset; it can only be inferred by the scale-invariance principle above, not measured directly.
- Long femurs specifically: no source in this session addressed whether femur-to-tibia ratio changes
  hip or knee flexion angles at any swing event. Bourgain's knee flexion amplitude figures (§3) and
  Lin 2023's hip/knee downswing peaks (§6) are the closest available baseline; applying them to a
  long-femur model is an extrapolation, not a validated match.
- **Recommendation:** treat the angle values in this document as directly applicable to the 189 cm
  model; do not attempt to invent a stature-scaling correction to the angles themselves without
  further primary-source support, since none was found and the scale-invariance argument is the
  standard default assumption in biomechanics absent contrary evidence.

---

## 13. Additional corroborating sources (pelvis/thorax velocity timing; clinical ROM context)

### 13.1 Steele KM, Roh EY, Mahtani G, et al. (2018), "Golf Swing Rotational Velocity: The Essential
Follow-Through," *Annals of Rehabilitation Medicine* 42(5):713. PMC6246863 / doi:10.5535/arm.2018.42.5.713.

Reports professional-golfer pelvis/upper-torso rotational velocity figures **numerically identical**
to those Zhou et al. 2022 (§1.2) present as their professional reference cohort (downswing peak
upper torso 551.7±47.6°/s; impact 458.5±73.0°/s; follow-through 929.2±185.1°/s; pelvis downswing peak
415.2±32.9°/s; impact 288.8±70.9°/s; follow-through 309.8±42.1°/s; X-prime downswing −183.4±41.4°/s,
impact −170.3±63.0°/s, follow-through −729.4±160.8°/s). **This is very likely the same underlying
professional-golfer dataset reused between the two papers** (Zhou 2022 built its Swing Performance
Index on this normative cohort) rather than two independent confirmations — treat as one data source
appearing in two publications, not corroboration from two separate samples. Steele et al.'s specific
contribution: peak upper-torso rotational velocity and peak X-prime occur **after impact, in the
follow-through**, for both amateurs and professionals, with amateurs significantly reduced versus
professionals (p<0.05) — the follow-through, not the downswing, carries the single fastest rotation
of the whole swing for the upper torso.

### 13.2 Beak SH, Choi A, et al. (2013), "Upper torso and pelvis linear velocity during the downswing
of elite golfers," *Biomedical Engineering Online* 12:13. PMC3599250 / doi:10.1186/1475-925X-12-13.
14 male professional golfers, age 29±8y, 8.2±4.8y career; peak clubhead speed 45.4±3.9 m/s;
**downswing duration 0.31±0.04 s**.

Linear (not angular) segment speed, with **timing as % of downswing** — useful for cross-checking
the animation's downswing timing curve even though the quantity itself is translational:
- Upper torso maximum linear speed 0.440±0.11 m/s, occurring at **59±26% of downswing**.
- Pelvis maximum linear speed 0.434±0.11 m/s, occurring at **47±23% of downswing** — i.e. the pelvis's
  peak linear speed leads the upper torso's by roughly 12 percentage points of downswing duration,
  consistent with the proximal-to-distal sequencing principle in §2.
- Segment-coupling: upper-torso/pelvis speed correlation r=0.97±0.02; pelvis's anterior/posterior
  linear motion led the upper torso's in 93% of trials.

### 13.3 Hsu et al. (2026), "The influence of sex on shoulder and hip joint resting position and
mobility in elite golfers," *Scientific Reports*. PMC12902067 / doi:10.1038/s41598-026-36493-3.
**Clinical/static resting-position and passive-ROM measures (not in-swing kinematics)** — included
for anatomical-budget context only, not as swing pose data:

| Measure | Male right | Male left | Female right | Female left |
|---|---|---|---|---|
| Shoulder internal rotation, resting position | 53.30 ± 10.37° | 77.51 ± 16.47° | 52.51 ± 15.08° | 58.30 ± 20.56° |
| Hip internal rotation, resting position | 29.02 ± 17.03° | 32.52 ± 13.65° | 14.64 ± 10.13° | 14.55 ± 7.59° |
| Hip straight-leg-raise ROM | 55.80 ± 14.85° | 60.37 ± 10.42° | 69.96 ± 12.32° | 69.09 ± 11.10° |

Note these clinical resting-position hip-internal-rotation values (~29–33° in males) are
**meaningfully lower** than the in-swing lead-hip internal-rotation peak of ~42–44° reported by Lin
et al. 2023 (§6) and the ~50° amplitude figure pooled by Bourgain 2022 (§3) — a reminder that
dynamic, loaded, swing-specific joint excursion can exceed passive clinical-exam ROM, so clinical
norms should not be used as a hard ceiling when animating the swing itself.

### 13.4 Hara D, Nakashima Y, et al. (2016), "Dynamic Hip Kinematics During the Golf Swing After
Total Hip Arthroplasty," *American Journal of Sports Medicine* 44(7):1801–9. In-vivo fluoroscopic
measurement: **≈50° of axial (internal/external) hip rotation on both lead and trail sides** during
the swing in this implant population — an independent (non-optical-motion-capture) method broadly
corroborating the ~40–50° hip axial rotation range reported by the other sources in §3/§6.
Cup-head translation during the swing was minimal (≈1.3–1.5 mm), with no bone-to-bone or
bone-to-implant contact at any swing phase — of limited direct relevance to this project beyond
confirming the ~50° hip rotation figure from a completely different measurement modality.

---

## Bibliography (all sources cited above, in order of first appearance)

1. Severin AC, Burkett BJ, McKean MR, et al. (2022). "Three-dimensional kinematics in healthy older
   adult males during golf swings." *Sports Biomechanics*. PMC7044058. doi:10.1080/14763141.2019.1649452.
2. Zhou JY, et al. (2022). "The Swing Performance Index: Developing a single-score index of golf
   swing rotational biomechanics quantified with 3D kinematics." *Frontiers in Sports and Active
   Living*. PMC9816382. doi:10.3389/fspor.2022.986281.
3. Grathwohl J, Sillevis R (2024). "Improving Golf Swing Kinematics in a 78-Year-Old Golfer with
   Lower Back Pain: A Case Report." *American Journal of Case Reports*. PMC11642117.
   doi:10.12659/AJCR.946077.
4. Wheare MJ, et al. (2021). "Reliability and Validity of the Polhemus Liberty System for Upper Body
   Segment and Joint Angular Kinematics of Elite Golfers." *Sensors* 21(13):4330. PMC8271493.
   doi:10.3390/s21134330.
5. Chen et al. (2024). "Does Overhead Squat Performance Affect the Swing Kinematics and Lumbar Spine
   Loads during the Golf Downswing?" *Sensors* 24(5). PMC10893031. doi:10.3390/s24041252.
6. Lin et al. (2023). "Lower Limb Biomechanics during the Golf Downswing in Individuals with and
   without a History of Knee Joint Injury." *Bioengineering* 10(2). PMC10215287.
7. Edwards N, Dickin C, Wang H (2020). "Low back pain and golf: A review of biomechanical risk
   factors." *Sports Medicine and Health Science* 2(1). PMC9219256. doi:10.1016/j.smhs.2020.03.002.
8. Bourgain M, Rouch P, Rouillon O, Thoreux P, Sauret C (2022). "Golf Swing Biomechanics: A
   Systematic Review and Methodological Recommendations for Kinematics." *Sports* 10(6):91.
   PMC9227529. doi:10.3390/sports10060091. (Systematic review of 92 kinematics articles; pooled
   Tables 6–10 values attributed to Murakami et al. and Kim et al. within it are cited as
   "Bourgain 2022, citing Murakami/Kim" since the primary papers' own text was not independently
   fetched in this session.)
9. White AA, Panjabi MM (1990). *Clinical Biomechanics of the Spine*, 2nd ed., J.B. Lippincott, p.107
   — segmental lumbar ROM table, retrieved via Wikipedia's "Lumbar vertebrae" article citation
   (secondary retrieval, flagged in §9).
10. McNally WJ, et al. (2019). "GolfDB: A Video Database for Golf Swing Sequencing." CVPR Workshops
    2019. Repository: github.com/wmcnally/golfdb (fetched directly).
11. Steele KM, Roh EY, Mahtani G, et al. (2018). "Golf Swing Rotational Velocity: The Essential
    Follow-Through." *Annals of Rehabilitation Medicine* 42(5):713. PMC6246863.
    doi:10.5535/arm.2018.42.5.713.
12. Beak SH, Choi A, Choi MT, Mun JH (2013). "Upper torso and pelvis linear velocity during the
    downswing of elite golfers." *Biomedical Engineering Online* 12:13. PMC3599250.
    doi:10.1186/1475-925X-12-13.
13. Hsu et al. (2026). "The influence of sex on shoulder and hip joint resting position and mobility
    in elite golfers." *Scientific Reports*. PMC12902067. doi:10.1038/s41598-026-36493-3.
14. Hara D, Nakashima Y, Hamai S, et al. (2016). "Dynamic Hip Kinematics During the Golf Swing After
    Total Hip Arthroplasty." *American Journal of Sports Medicine* 44(7):1801–9.
15. Horan SL, et al. — cited only secondhand via Bourgain 2022 (§2, §10) for the head/pelvis/torso
    kinematic-sequence and head-rotation-speed claim; primary paper not independently located or
    fetched in this session — **flagged as unverified**, do not treat as independently confirmed.
16. McHardy A, Pollard H (2005) and the Jobe/Pink/Perry/Kao/Bechler five-phase EMG lineage — carried
    over by reference from `docs/research/01-phase-taxonomy-and-timing.md` for phase-boundary
    consistency; not re-fetched in this session.
17. Cheetham PJ, Rose GA, Hinrichs RN, et al. and Neal RJ, et al. — the classic golf kinematic-
    sequence originators, referenced only as named/discussed inside Bourgain 2022's review text
    (§2); **their primary papers could not be located directly in Europe PMC/PubMed in this session**
    (search returned only recent unrelated kinematic-sequence papers) — a genuine access gap, not
    just unsummarised text.

---

## 14. Coverage summary against the 12 requested items

| # | Item | Coverage |
|---|---|---|
| 1 | Pelvis rotation (address/top/impact/finish, peak velocity+timing) | **Good** — top/impact/finish angles (§1.1), peak velocities by phase (§1.1/1.2/13.1), % downswing timing for peak linear speed (§13.2). Address-specific pelvis rotation angle only from a single n=1 case report (§1.3) — weak for address specifically. |
| 2 | Thorax rotation (as above) | **Good** — same sources as pelvis; X-factor/X-prime relates the two directly. |
| 3 | Spine segmentation; lumbar rotation limit | **Good** — lumbar limit figure sourced (§9); thoracic-specific total ROM figure not found (flagged gap). |
| 4 | Lead/trail shoulder (abd/add, flex/ext, IR/ER) | **Partial** — lead shoulder well covered event-by-event (§4); trail shoulder only as pooled amplitude (§3), no event-resolved trail-shoulder table found despite searching. |
| 5 | Elbows (lead straight-arm question, trail at top) | **Partial** — only amplitude figures (lead 26°, trail 95°, §3), consistent with "lead arm stays close to straight, trail elbow bends substantially at top" but no absolute degree value at any single event for either elbow — a genuine gap despite repeated search attempts. |
| 6 | Wrists (flex/ext, dev, cock angle, release timing) | **Good** — full event-resolved table both sides (§4); release/timing curve not separately isolated but top-of-backswing and impact values bound it. |
| 7 | Hips/knees (flex at address, knee flexion through swing, hip IR/ER both sides) | **Good** — §1.1, §3, §6, §13.3/13.4 give multiple independent datasets; address-specific knee/hip flexion values not found as a clean standalone figure (only address trunk/pelvis figures exist), flagged gap. |
| 8 | Posture (forward spine tilt at address, side bend at impact) | **Partial** — a single clear address trunk-flexion figure (45°, §7); side bend at impact only isolated for the lumbar segment (21°, §8), not whole-trunk. |
| 9 | Head (position/stability) | **Weak** — only a provisional, unverified rotational-speed figure (§10); no translation/sway data found at all. |
| 10 | Public 3D mocap datasets | **Resolved as "none found"** — GolfDB exists but is 2D video, non-commercial licence, not joint-angle data (§11); CMU database unconfirmed due to a TLS failure. |
| 11 | Anthropometry/stature scaling | **Resolved as "no golf-specific source found"** — answered via the general angle-invariance principle in biomechanics, explicitly flagged as reasoned inference rather than a directly-cited golf-specific finding (§12). |

