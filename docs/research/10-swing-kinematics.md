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

## Status: IN PROGRESS — being written incrementally, do not treat as final until this line is removed.

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

