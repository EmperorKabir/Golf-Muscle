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

