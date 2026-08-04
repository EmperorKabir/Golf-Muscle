# Shoulder girdle, arm, forearm and grip activation by swing phase

Lead = left side, trail = right side, right-handed golfer, throughout.

## Three warnings that govern everything below

### 1. The units are not interchangeable

Four incompatible normalisation methods appear across the upper-limb literature:

- **%MMT** — manual muscle test reference. The entire Jobe / Pink / Perry / Kao / Farber (Centinela →
  Kerlan-Jobe) series uses this. Later authors routinely re-cite these values as "%MVC"; that is their
  error, not the original papers'.
- **%MVC** — isometric maximum voluntary contraction reference (Glazebrook, Pezarat-Correia, Sorbie).
- **Raw µV, unnormalised** — Bochnia 2024 and Grieß 2026 state explicitly that "no normalization was
  performed". These values cannot be converted to a percentage of anything.
- **Onset timing only** — Verikas 2016 reports activation sequence, no amplitude.

A muscle at "60%" in one study is not the same quantity as "60%" in another. Every figure below is
labelled with its unit. **Do not merge the µV studies onto the same axis as the percentage studies.**

### 2. The literature resolves 5 phases, not 9

Verbatim phase definitions (Pink M, Perry J, Jobe FW 1993; independently confirmed for phases 1–2 by
Bechler et al. 1995):

| # | Phase | Boundary definition (verbatim) |
|---|---|---|
| 1 | Take-away | "from address to the ball to the end of the backswing" |
| 2 | Forward swing | "from the end of the backswing until the club is horizontal" |
| 3 | Acceleration | "from horizontal position of the club to ball contact" |
| 4 | Early follow-through | "from ball contact to horizontal club position" |
| 5 | Late follow-through | "from horizontal club position to the end of the swing" |

Mapping onto the 9-phase model requested:

| 9-phase bin | Status in the literature |
|---|---|
| Address | **Boundary instant.** Only Glazebrook 1994 samples it. |
| Takeaway / early backswing | Take-away (phase 1) |
| Late backswing | Take-away (phase 1) — **same bin, not resolved separately** |
| Top / transition | **Boundary instant** between phases 1 and 2 |
| Early downswing | Forward swing (phase 2) |
| Late downswing / acceleration | Acceleration (phase 3) — begins strictly at **club horizontal**, not at a time fraction |
| Impact | **Boundary instant** between phases 3 and 4 (= ball contact) |
| Early follow-through | Phase 4 |
| Late follow-through | Phase 5 |

Consequences the app must respect: **early and late backswing are not distinguishable from published
data** — they are one bin. **Address, top of backswing and impact are never sampled as bins** by any
shoulder or scapular study; the sole exception is Glazebrook 1994, which samples address and contact for
the forearm. Anything the app displays at those three instants is interpolation, not measurement.

Note also that "acceleration" in this literature is *not* the whole downswing. It starts at club-horizontal,
which is roughly the last third of the downswing. The Jobe 1986 paper used **four** segments, not five —
the 5-phase scheme was codified later — and its segment names could not be recovered (paywalled).

### 3. The shoulder data is one dataset from 1986–1990, never replicated

Every review from 2004 to 2025 (Kim 2004, McHardy & Pollard 2005, Escamilla & Andrews 2009,
Marta et al. 2012) re-cites the same Kerlan-Jobe fine-wire dataset. **No modern EMG study has
re-measured the shoulder prime movers or rotator cuff in golf.** The forearm has been re-measured
(Farber 2009, Sorbie 2016/2017, Robinson 2023, Bochnia 2024, Grieß 2026); the shoulder has not.

---

## Shoulder prime movers and rotator cuff

Source: **Pink M, Jobe FW, Perry J. Electromyographic analysis of the shoulder during the golf swing.
Am J Sports Med. 1990;18(2):137-140. PMID 2343980.** 13 professional golfers (6 male, 7 female),
indwelling fine-wire electrodes, 8 muscles bilaterally. Values are **%MMT**.

Confidence note: these values were extracted from a scanned copy and cross-checked against
McHardy & Pollard 2005 Table 3, which independently reproduces the peak cells. Nine overlapping cells
agree exactly (9/9). Non-peak cells rest on the single extraction and carry slightly lower certainty.

### Trail (right) shoulder — %MMT

| Muscle | Take-away | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 12 | 64 | **93** | 74 | 37 |
| Subscapularis | 16 | 49 | **68** | 64 | 56 |
| Supraspinatus | **25** | 14 | 12 | 7 | 7 |
| Infraspinatus | **27** | 13 | 7 | 12 | 9 |
| Anterior deltoid | 5 | **21** | 10 | 11 | 8 |
| Middle deltoid | 2–8 across all phases, no pattern | | | | |
| Posterior deltoid | 5–24 across all phases, no pattern | | | | |

### Lead (left) shoulder — %MMT

| Muscle | Take-away | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 21 | 18 | **93** | 74 | 39 |
| Subscapularis | 33 | 29 | **41** | 23 | 35 |
| Supraspinatus | 21 | 21 | 18 | **28** | 28 |
| Infraspinatus | 14 | 16 | 27 | **61** | 40 |
| Anterior deltoid | 13 | 9 | 10 | 21 | **26** |
| Middle deltoid | 2–8 across all phases, no pattern | | | | |
| Posterior deltoid | 5–24 across all phases, no pattern | | | | |

**Flagged anomaly:** pectoralis major reads identically on both sides at acceleration (93) and at early
follow-through (74). Both the scanned original and McHardy's Table 3 give these figures, but two identical
cross-side values at two separate phases is unusual and may be a transcription artefact in the source
table rather than a true bilateral identity. Treat the lead-side pec major acceleration/early-FT figures as
lower-confidence than the trail side.

### Verbatim qualitative findings

- Pink 1990 abstract: "the infraspinatus and supraspinatus act predominantly at the extremes of shoulder
  range of motion, the subscapularis and pectoralis major during acceleration, the latissimus dorsi during
  forward swing, and the anterior deltoid during forward swing and follow-through. The middle and posterior
  deltoids appear to be relatively noncontributory, without any specific timing patterns."
- Pink 1990 on middle deltoid, verbatim: "low levels of activity for all phases of the activity (2% to 8% MMT)."
- Pink 1990 on posterior deltoid, verbatim: "low activity levels and no significant differences nor pattern of
  activity throughout all phases for both the right and left sides (5% to 24% MMT)."
- Jobe, Moynes & Antonelli 1986 (PMID 3777315, 7 male professionals, bilateral fine-wire): "The
  subscapularis was more active than any other muscle throughout the swing. The cuff muscles on the right
  side showed as much activity overall as those on the left."

### Teres minor and teres major — no data exists

Neither muscle was instrumented in any golf EMG study. The Jobe/Pink rotator cuff set was supraspinatus,
infraspinatus and subscapularis only. A targeted search returned no teres-minor golf EMG study; the only
"teres major + golf" publication is a single case report of traumatic tendon avulsion (Spinner, Speer &
Mallon, Am J Sports Med 1998;26:847-849, PMID 9850790). **Do not estimate values for these two muscles.**

---

## Scapular muscles

Source: **Kao JT, Pink M, Jobe FW, Perry J. Electromyographic analysis of the scapular muscles during a
golf swing. Am J Sports Med. 1995;23(1):19-23. PMID 7726345.** 15 competitive male golfers, 4 muscle
groups bilaterally (levator scapulae, rhomboids, trapezius, serratus anterior).

**Access failure, stated plainly:** the Kao 1995 full text is paywalled with no open-access copy anywhere
(Unpaywall confirms `is_oa: false`; ResearchGate, Academia.edu and Scribd all blocked). Its complete
per-phase %MMT table could not be obtained. The numeric values below are only those that surface in
McHardy & Pollard 2005's Table 3, which lists the **two most active muscles per side per phase** — so
these are peak cells only, not full curves.

### Numeric values recovered (%MMT, via McHardy & Pollard 2005 Table 3)

| Phase | Lead (left) | Trail (right) |
|---|---|---|
| Back swing | upper serratus 30 | **upper trapezius 52**, middle trapezius 37 |
| Forward swing | **rhomboid 68**, middle trapezius 51 | upper serratus 58 |
| Acceleration | levator scapulae 62 | **upper serratus 69** |
| Early follow-through | — | — |
| Late follow-through | — | serratus anterior (upper + lower) 40 |

Cells marked "—" mean that side's two most-active muscles in that phase were *not* scapular muscles
(they were pectoralis major, infraspinatus or subscapularis), so no scapular figure is published for them.

### Qualitative pattern — Kao 1995 abstract, verbatim

> "In the trailing arm, the levator scapulae elevates while the rhomboid muscles retract the scapula during
> takeaway; both then stabilize the scapula through the remainder of the swing. In the leading arm, these
> muscles retract the scapula during forward swing and acceleration. The trapezius muscle in the trailing arm
> also demonstrates high activity during takeaway to aid in scapular retraction. In the leading arm, trapezius
> activity is high in forward swing and through the remainder of the swing to promote scapular retraction.
> The serratus anterior muscle activity is high in the trailing arm during forward swing and through the
> remainder of the swing to maximize scapular protraction. In the leading arm, the serratus anterior muscle
> has constant activity through all phases of the swing, which may explain the clinical scenario of muscle
> fatigue in high demand golfers."

Derived per-muscle summary:

| Muscle | Lead peak phase | Trail peak phase |
|---|---|---|
| Trapezius (upper/middle/lower) | Forward swing → remainder | Take-away |
| Rhomboids | Forward swing + acceleration | Take-away, then stabilise |
| Levator scapulae | Forward swing + acceleration | Take-away, then stabilise |
| Serratus anterior | **Constant across all phases** | Forward swing → remainder |

Kao 1995 distinguished upper, middle and lower trapezius; the abstract does not break the three apart, and
the only numeric cells recovered are upper (52) and middle (37) trapezius on the trail side at back swing.
**Lower trapezius has no recovered numeric value at any phase.** Rhomboid major vs minor is not
distinguished by any source. Serratus anterior is reported as "upper serratus" and "upper + lower" in
different cells of McHardy's table, implying separate digitation electrodes, but the split is not recoverable.

---

## Latissimus dorsi — peak phase genuinely disputed

Three sources, two answers, unresolved:

- **Jobe, Moynes & Antonelli 1986** (PMID 3777315): latissimus dorsi and pectoralis major "seemed to
  provide power bilaterally, with marked activity during the **acceleration** phase."
- **Pink, Jobe & Perry 1990** (PMID 2343980), described as an expansion of the 1986 pilot: latissimus dorsi
  acts "during **forward swing**."
- **Marta et al. 2012** review, synthesising 19 studies: "The pectoralis major, subscapularis and latissimus
  dorsi muscles of both sides showed their peak activity during the **acceleration** phase."

Two of three say acceleration; the intermediate 1990 paper says forward swing. No numeric %MMT value for
latissimus dorsi was recoverable from any source. Report the range, do not pick one.

---

## Arm — biceps, triceps, brachioradialis

Golf-specific data here is thin and rests largely on one small conference study.

**Pezarat-Correia P, Cabri J, Fernandes O, Sousa JP. "Electromyographic Analysis of the Dominant Upper
Limb During the Golf Swing." Proc ECSS Lausanne 2006;3(1):70-85.** n=3 low-handicap golfers, pitch iron,
**trail (dominant) arm only**, %MVC, 3-phase scheme (backswing / downswing / follow-through).

| Muscle (trail arm) | Peak %MVC | Phase |
|---|---|---|
| Brachioradialis | **45** | Backswing |
| Biceps brachii | **26** | Backswing |
| Triceps brachii, long head | **50** | Downswing |
| Latissimus dorsi | **53** | (highest of 12 muscles recorded) |

The paper states elbow flexors are "strongest activation during the BS ... and silenced before the DS
initiation", and that elbow extensors "presented the highest EMG activation" during the downswing.
**n=3 — treat as indicative, not established.**

### Raw µV studies (NOT %MVC — do not merge with the table above)

Bochnia et al. 2024 (BMC Musculoskelet Disord 25:668, PMID 39187838, n=30) and Grieß et al. 2026
(BMC Musculoskelet Disord 27:175, PMID 41673660, n=40) both measured biceps brachii bilaterally in raw
microvolts across the 5-phase scheme. Both found biceps rising **monotonically to a peak in late
follow-through**, on both sides — e.g. Bochnia lead arm mean µV: 13.9 → 21.6 → 34.9 → 77.8 → 155.7.

This directly contradicts Pezarat-Correia's finding of a backswing biceps peak. The conflict may be
methodological (raw amplitude vs %MVC, n=3 vs n=30, 3-phase vs 5-phase binning) and is **unresolved**.

### Gaps stated plainly

- **Lead-arm triceps brachii: no golf data of any kind.** Biomechanically the lead elbow must resist
  flexion torque from top of backswing through impact, implying sustained activity, but nothing quantifies it.
- **Lead-arm brachioradialis: no golf EMG data.** One clinical case report only (Nakamura, Abe & Kumano,
  J Hand Surg Asian Pac Vol 2019 — acute compartment syndrome from a brachioradialis haematoma in
  the lead forearm during golf, compartment pressure 120 mmHg), which establishes mechanical loading
  but is not activation data.
- **There is no Jobe/Perry/Pink elbow paper.** Confirmed against McHardy & Pollard's reference list: the
  entire Kerlan-Jobe golf series covers shoulder, scapula, trunk, hip and knee only. The group's forearm
  paper is Farber 2009, below.

---

## Supinator — no data

**No golf EMG study has ever measured supinator, on either side.** Targeted searching returned zero papers
combining the two terms. The nearest proxy is an "extensor–supinator mass" composite electrode in baseball
pitching (van Trigt et al., Front Sports Act Living 2021, PMCID PMC8669487), showing moderate activity
(21–40% of normalised max) at maximal external rotation in the throwing arm — **not golf, composite
electrode, not the isolated muscle.** Kinematics imply the lead supinator works through impact and early
follow-through (the lead forearm supinates while the trail forearm pronates), but this is inference from
motion, not measurement. **Do not assign a measured value.**

---

## Pronator teres — the best skill-level evidence in the whole upper limb

**Farber AJ, Smith JS, Kvitne RS, Mohr KJ, Shin SS. Electromyographic analysis of forearm muscles in
professional and amateur golfers. Am J Sports Med. 2009;37(2):396-401. PMID 19022991.** Kerlan-Jobe
Clinic. n=10 professional, n=10 amateur, male, right-handed, fine-wire EMG, **%MMT**.

Pronator teres was the **only** muscle to reach significance in the study, and the direction inverts by side:

| Side | Phase | Amateur %MMT | Professional %MMT | p |
|---|---|---|---|---|
| Trail | Forward swing | **120.9** | 57.4 | .04 |
| Trail | Acceleration | 104.8 | 53.1 | .08 (trend) |
| Lead | Acceleration | 36.3 | **88.1** | .03 |
| Lead | Early follow-through | 28.8 | 58.1 | .06 (trend) |

Interpretation: **amateurs over-recruit the trail pronator early in the downswing; professionals recruit the
lead pronator later, through acceleration into follow-through.** The authors tie the amateur trail-side
over-recruitment to medial epicondylitis risk. Note the amateur trail value **exceeds 100% MMT** — dynamic
ballistic EMG routinely exceeds the static reference contraction.

Farber also recorded FCR, FCU and ECRB bilaterally but reported **no significant differences** for them;
their numeric values are in the paywalled full text and could not be recovered.

Kinematic corroboration (McHardy & Pollard 2005): at impact there is "left arm supination and right arm
pronation", continuing through early follow-through as "left arm external rotation and right arm internal
rotation."

---

## Wrist flexors and extensors

### Glazebrook et al. 1994 — the only %MVC forearm dataset

**Glazebrook MA, Curwin S, Islam MN, Kozey J, Stanish WD. Medial epicondylitis: an electromyographic
analysis and an investigation of intervention strategies. Am J Sports Med. 1994;22(5):674-679. PMID
7810792.** Four swing phases including address and contact. Measures muscle *groups*, not individual
muscles. **Arm side is not stated in the retrievable abstract — a significant limitation.**

| Muscle group | Address | ... | Contact |
|---|---|---|---|
| Common extensor mass | **33.59% MVC** | persistent throughout | **58.77% MVC** |
| Common flexor mass | — | — | **90.77% MVC** ("flexor burst") |

Key distinction: the **extensors rise gradually** from address to contact; the **flexors fire as a discrete
burst at contact**. Intermediate-phase values are not given in the abstract.

Symptomatic (medial epicondylitis) golfers showed significantly greater flexor activity than asymptomatic
golfers at address and through the swing — magnitude not quantified in the abstract. Forearm braces and
oversized grips showed no significant effect on EMG magnitude or pattern.

### Robinson et al. 2023 — the only direct lead-vs-trail statistical comparison

**Robinson PG, Carson HJ, Richards J, Murray A, Duckworth AD, Campbell D. J Sports Sci.
2023;41(17):1596-1604. PMID 37983261.** n=15 sub-elite golfers (mean handicap 1.5±2.2), extensor carpi
ulnaris, three clubs, three phases.

- **Trail ECU > lead ECU during downswing**, across all three clubs (p<0.001)
- **Lead ECU > trail ECU during backswing** (p<0.001) **and follow-through** (p=0.024)
- No significant correlation between downswing EMG and clubhead kinematics at impact
- Authors attribute the asymmetric clinical injury pattern to this difference

Magnitudes are not in the abstract; the full text was 403-blocked on all four mirrors attempted.

### Raw µV studies — Bochnia 2024 (n=30) and Grieß 2026 (n=40)

Unnormalised microvolts, 5-phase scheme, both arms. Baseline (standard grip / steel shaft) condition:

**Flexor carpi ulnaris, mean µV** (Bochnia / Grieß):

| Side | Take-away | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Lead | 76.6 / 93.9 | 123.0 / 152.3 | 115.4 / 155.2 | **138.5 / 185.1** | 120.2 / 158.2 |
| Trail | 61.2 / 60.4 | 68.7 / 68.5 | 107.0 / 131.5 | **201.4 / 217.3** | 158.0 / 162.7 |

**Extensor carpi radialis brevis, mean µV** (Bochnia / Grieß):

| Side | Take-away | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Lead | 65.3 / 88.9 | 48.2 / 62.5 | 55.0 / 84.3 | **142.2 / 145.8** | 130.6 / 139.2 |
| Trail | **98.5 / 93.9** | 84.0 / 91.9 | 48.4 / 66.5 | 60.4 / 103.1 | 129.8 / 121.4 |

Note the **side asymmetry in ECRB**: the trail side loads early (take-away) then falls through acceleration;
the lead side is quiet early and loads after impact. Both studies reproduce this independently.

Equipment effects (both studies, statistically significant): an ergonomic grip significantly reduced **trail**
pronator teres in forward swing, acceleration and early follow-through (Bochnia); graphite shafts reduced
**lead** pronator teres in late follow-through vs steel (p=.009, Grieß).

### Skill level — Sorbie et al. 2016

**Sorbie GG, Hunter HH, Grace FM, Gu Y, Baker JS, Ugbolue UC. Res Sports Med. 2016. PMID 27267082.**
n=15, ECRB and FDS, lead and trail, three grip sizes, 7-iron: **amateurs produced significantly greater
forearm muscle activity than professionals during both backswing and downswing, across all three grip
sizes (p<0.05).** Grip size itself had no significant effect. Absolute values not in the abstract.

A companion study (Sorbie et al., Res Sports Med 2017, PMID 28819996) found no significant EMG
difference between gloved and ungloved conditions.

### Muscles with no golf data

- **Flexor digitorum profundus** — no golf-specific study.
- **Extensor carpi radialis longus** — no study isolating it.
- **Extensor digitorum** — recorded by Verikas 2016 but only for onset timing, no amplitude.
- **Flexor carpi radialis** — recorded by Farber 2009 and Verikas 2016; no per-phase amplitude published.
- **Intrinsic hand muscles** (interossei, lumbricals, thenar, hypothenar) — **no golf EMG study exists.**

---

## Grip force

Only three studies exist. None publishes an absolute force-vs-phase curve for both hands.

### Langlais SM, Broker JP. Grip pressure distributions and associated variability in golf: a two-club comparison. Sports Biomechanics. 2014;13(2):109-122. PMID 25122996.

n=8 low-handicap golfers (USGA index 0–7), instrumented grip measuring lead-hand, trail-hand and
individual finger forces, driver and 7-iron.

- **Lead-hand force mirrors the total grip-force profile** across the whole swing, for both clubs.
- **Trail-hand force is substantially lower than lead-hand throughout — except at take-away**, where the
  two hands are similar. The trail hand contributes proportionally more early, then falls away.
- Dominant contribution comes from the **lead hand's last three fingers** (middle, ring, little).
- 4 of 8 golfers showed a distinct **trail index-finger spike (~20% of total force) immediately pre-impact**.
- Within-golfer repeatability: SD <7% of total force before impact; ~5% CV at impact on the 7-iron.
- Cross-club profile correlation r²=0.86 overall; lead hand r²=0.90, trail hand r²=0.73 — **the lead hand's
  pattern is far more club-invariant than the trail hand's.**
- Timing: "within-swing force variability was greatest during club acceleration, but dramatically decreased
  at impact" — the pattern **converges** at impact even as magnitude fluctuates most during the downswing.
- **No absolute force units (N/kg/lb) are reported** — profiles are normalised.

### Choi H, Park S. Three Dimensional Upper Limb Joint Kinetics of a Golf Swing with Measured Internal Grip Force. Sensors. 2020;20(13):3672. PMID 32630024.

n=9 professional males, driver, custom axially-separated grip with an embedded 6-axis force/torque sensor.

- **Trail-hand torque is roughly threefold greater than lead-hand torque.**
- Both hands exert simultaneous opposing counterforces against each other throughout the swing.
- Downswing shows "backward and upward torque ... followed by abrupt reversal" around impact.
- **Lead-arm joint force/torque onset and peak precede the trail arm's by roughly 50–200 ms**; trail-arm
  peaks cluster around impact and are larger in magnitude.
- Data presented graphically; **no absolute Newton/kg values extractable.**

### Budney DR. Measuring grip pressure during the golf swing. Research Quarterly. 1979;50(2):272-277. PMID 472468.

The earliest grip-pressure study. PubMed holds **no abstract**; full text is not available through any
open-access route attempted. Numeric values, phase breakdown and lead/trail comparison **could not be
retrieved**. Flagged rather than estimated.

### Net position on grip force

The lead hand carries **more absolute grip force** through most of the swing; the trail hand generates
**more torque**, concentrated near impact. These are different mechanical quantities from different studies
and **must not be merged into a single number**. The literature does not support a published magnitude in
Newtons for either hand at any phase. Whether grip pressure rises gradually or spikes at impact is
**not settled**: Langlais & Broker show variability peaking during acceleration and *collapsing* at impact
(a convergence, not a spike), while the trail index-finger spike appears in only half their sample.

---

## Which upper-limb muscles peak where

Well-supported (two or more independent sources):

| Peak phase | Muscles |
|---|---|
| Take-away | Trail supraspinatus (25), trail infraspinatus (27), trail upper trapezius (52), trail middle trapezius (37), trail rhomboids, trail levator scapulae, trail ECRB |
| Forward swing | Trail pectoralis major (64), lead rhomboid (68), lead middle trapezius (51), trail upper serratus (58), trail pronator teres (amateurs, 120.9) |
| Acceleration | **Pectoralis major bilaterally (93)** — highest value recorded in the shoulder; trail subscapularis (68), lead levator scapulae (62), trail upper serratus (69), lead pronator teres (professionals, 88.1) |
| Impact (instant) | Common flexor burst (90.77% MVC), common extensor (58.77% MVC) |
| Early follow-through | Lead infraspinatus (61), trail subscapularis (64), lead supraspinatus (28), FCU bilaterally (µV studies) |
| Late follow-through | Trail subscapularis (56), lead infraspinatus (40), lead anterior deltoid (26), biceps bilaterally (µV studies) |

The two claims the user's brief proposed are **both confirmed, with a correction**: trail pectoralis major
and subscapularis do peak in the downswing (specifically the acceleration sub-phase) — but pectoralis major
peaks at the *same* value bilaterally, not trail-dominantly. Wrist flexors do peak near impact
(Glazebrook's flexor burst at contact).

**However, "peak near impact" is not a universal rule.** Robinson 2023 puts trail ECU's peak in the
downswing and lead ECU's in backswing and follow-through. The two large µV studies put most
muscle/side combinations' raw amplitude peak in **late follow-through**. Model this per muscle and per
side, never as one global rule.

---

## Lead vs trail, summarised

- **Rotator cuff.** Trail cuff (supraspinatus, infraspinatus) fires early, in take-away, then goes quiet. Lead
  cuff fires late, peaking in follow-through (lead infraspinatus 61 at early FT vs trail's 12). The lead
  shoulder decelerates the swing; the trail shoulder positions it.
- **Subscapularis** is the exception: high on **both** sides throughout, trail-dominant (68 vs 41 at
  acceleration), and the most consistently active cuff muscle in the swing.
- **Scapular muscles.** A clean temporal split: trail scapular muscles peak in **take-away** (retraction and
  elevation to set the backswing); lead scapular muscles peak in **forward swing and acceleration**
  (retraction to pull through). The lead serratus anterior is the outlier — **constant across all phases**,
  which Kao 1995 links to fatigue in high-volume golfers.
- **Pronator teres inverts with skill.** Amateurs load the trail pronator early; professionals load the lead
  pronator late. This is the single clearest skill-level signature in the upper limb.
- **ECRB** loads early on the trail side and late on the lead side.
- **ECU** is trail-dominant in the downswing, lead-dominant in backswing and follow-through.
- **Grip.** Lead hand carries the force, trail hand supplies the torque near impact.
- **Injury laterality corroborates the asymmetry**: over 90% of golfers' shoulder problems involve the lead
  shoulder; lead-shoulder injuries are roughly 3× as common as trail (Kim, Millett, Warner & Jobe,
  Am J Sports Med 2004;32(5):1324-1330).

---

## Professional vs amateur

Evidence is genuinely thin and is **almost entirely forearm**, not shoulder.

- **Farber 2009** (fine-wire, pro vs amateur): the pronator teres inversion above. The only significant
  skill-level upper-limb finding in the literature.
- **Sorbie 2016** (surface, pro vs amateur): amateurs produce significantly greater forearm activity than
  professionals in both backswing and downswing, across all grip sizes.
- Pattern across both: **amateurs work the forearm harder and earlier**; professionals recruit later and
  more selectively, and on the lead side.
- **Jobe, Perry & Pink 1989** (PMID 2624291) is **not** a skill-level study — it compares male and female
  *professionals*. Its finding: women showed slightly more activity in take-away and forward swing, men
  more in acceleration and follow-through, but "an independent two-tailed t-test (P = 0.05) showed these
  differences **not to be statistically significant**." Cite it for similarity, not difference.
- **No shoulder or scapular pro-vs-amateur EMG comparison exists.** Marta et al. 2012 states the gap
  directly: "there is a lack of studies on average golf players, since most studies were executed on
  professional or low handicap golfers."
- Abernethy B, Neal RJ, Parker AW et al., "Expert-novice differences in muscle activity during the golf
  swing", in Cochran (ed.) *Science and Golf* — exists but year, publisher and pages **could not be
  verified**; treat as low-confidence.

---

## Magnitude bands — the assumed scheme is not verified

The commonly-quoted banding (<20% low, 20–40% moderate, 40–60% high, >60% very high) **could not be
traced to any golf EMG paper.** What the literature actually does:

- **Pink, Perry & Jobe 1993** uses a **binary, %MMT-based** cutoff: "below 30% of maximal muscle test"
  = relatively low; "above 30% maximal muscle test" = relatively high.
- **Glazebrook 1994** reports raw %MVC with **no bands at all**.
- **Marta et al. 2012** and **McHardy & Pollard 2005** use purely qualitative words ("high", "moderate to
  low") with **no numeric cutoffs**.
- **Kao 1995** uses only relative language ("high activity", "constant activity", "reduced").

If the app uses a four-tier band, attribute it to general sports-EMG convention, **not** to any golf paper.

**Values above 100% are real and expected.** Marta et al. 2012 notes wrist flexor activity "above the
maximal voluntary contraction"; Farber 2009's amateur trail pronator teres reads 120.9% MMT. Dynamic
ballistic EMG routinely exceeds a static isometric reference. **The app must not hard-clamp activation at
100%** — doing so would silently truncate the single highest-activation muscle in the swing.

---

## What could not be verified

1. **Kao 1995 full per-phase scapular table** — paywalled, no OA copy. Only peak cells recovered, via
   McHardy's Table 3. This is the largest single data gap.
2. **Lower trapezius** — no numeric value at any phase, either side.
3. **Rhomboid major vs minor**, and **serratus anterior upper vs lower digitations** — not separable.
4. **Teres minor, teres major, supinator** — no golf EMG data exists at all. Do not estimate.
5. **Flexor digitorum profundus, ECRL, extensor digitorum, intrinsic hand muscles** — no per-phase data.
6. **FCR, FCU, ECRB numeric values in Farber 2009** — non-significant, values withheld in abstract, full
   text paywalled.
7. **Glazebrook 1994 arm side** — not stated in the retrievable abstract, so the flexor burst (90.77% MVC)
   cannot be attributed to lead or trail with confidence. Its intermediate-phase values are also unpublished.
8. **Robinson 2023 ECU magnitudes** — significance reported, magnitudes not; full text 403 on all mirrors.
9. **Budney 1979 grip pressure values** — no abstract on PubMed, no accessible full text.
10. **Jobe 1986's four segment names/boundaries** — paywalled; the 5-phase scheme postdates it.
11. **Latissimus dorsi peak phase** — sources disagree (forward swing vs acceleration); no numeric value.
12. **Biceps peak phase** — Pezarat-Correia (n=3, %MVC) says backswing; Bochnia/Grieß (n=30/40, raw µV)
    say late follow-through. Unresolved, and confounded by differing normalisation.
13. **Pectoralis major bilateral identity at acceleration (93/93) and early FT (74/74)** — possible
    transcription artefact, flagged above.
14. **Whether foot-switches were used** in the golf papers — this is a hallmark of the same lab's gait
    studies; no golf paper confirms it. Cinematography with electronic synchronisation is confirmed.

## Primary citations

1. Jobe FW, Moynes DR, Antonelli DJ. Rotator cuff function during a golf swing. Am J Sports Med. 1986;14(5):388-392. PMID 3777315.
2. Jobe FW, Perry J, Pink M. Electromyographic shoulder activity in men and women professional golfers. Am J Sports Med. 1989;17(6):782-787. PMID 2624291.
3. Pink M, Jobe FW, Perry J. Electromyographic analysis of the shoulder during the golf swing. Am J Sports Med. 1990;18(2):137-140. PMID 2343980.
4. Pink M, Perry J, Jobe FW. Electromyographic analysis of the trunk in golfers. Am J Sports Med. 1993;21(3):385-388. PMID 8346752.
5. Glazebrook MA, Curwin S, Islam MN, Kozey J, Stanish WD. Medial epicondylitis: an electromyographic analysis and an investigation of intervention strategies. Am J Sports Med. 1994;22(5):674-679. PMID 7810792.
6. Kao JT, Pink M, Jobe FW, Perry J. Electromyographic analysis of the scapular muscles during a golf swing. Am J Sports Med. 1995;23(1):19-23. PMID 7726345.
7. Bechler JR, Jobe FW, Pink M, Perry J, Ruwe PA. Electromyographic analysis of the hip and knee during the golf swing. Clin J Sport Med. 1995;5(3):162-166. PMID 7670971.
8. Kim DH, Millett PJ, Warner JJP, Jobe FW. Shoulder injuries in golf. Am J Sports Med. 2004;32(5):1324-1330.
9. McHardy A, Pollard H. Muscle activity during the golf swing. Br J Sports Med. 2005;39(11):799-804. PMID 16244187. PMCID PMC1725059.
10. Pezarat-Correia P, Cabri J, Fernandes O, Sousa JP. Electromyographic analysis of the dominant upper limb during the golf swing. Proc ECSS Lausanne. 2006;3(1):70-85.
11. Farber AJ, Smith JS, Kvitne RS, Mohr KJ, Shin SS. Electromyographic analysis of forearm muscles in professional and amateur golfers. Am J Sports Med. 2009;37(2):396-401. PMID 19022991.
12. Marta S, Silva L, Castro MA, Pezarat-Correia P, Cabri J. Electromyography variables during the golf swing: a literature review. J Electromyogr Kinesiol. 2012;22(6):803-813. PMID 22542769.
13. Langlais SM, Broker JP. Grip pressure distributions and associated variability in golf: a two-club comparison. Sports Biomech. 2014;13(2):109-122. PMID 25122996.
14. Sorbie GG, Hunter HH, Grace FM, Gu Y, Baker JS, Ugbolue UC. An electromyographic study of the effect of hand grip sizes on forearm muscle activity and golf performance. Res Sports Med. 2016. PMID 27267082.
15. Verikas A, Vaiciukynas E, Gelzinis A, Parker J, Olsson MC. Electromyographic patterns during golf swing: activation sequence profiling and prediction of shot effectiveness. Sensors. 2016;16(4):592. PMID 27120604.
16. Sorbie GG, Darroch P, Grace FM, Gu Y, Baker JS, Ugbolue UC. Commercial golf glove effects on golf performance and forearm muscle activity. Res Sports Med. 2017. PMID 28819996.
17. Choi H, Park S. Three dimensional upper limb joint kinetics of a golf swing with measured internal grip force. Sensors. 2020;20(13):3672. PMID 32630024.
18. Robinson PG, Carson HJ, Richards J, Murray A, Duckworth AD, Campbell D. What differences exist between the lead and trail wrist in extensor carpi ulnaris activity and golf swing joint kinematics in sub-elite golfers? J Sports Sci. 2023;41(17):1596-1604. PMID 37983261.
19. Bochnia JM, Bockholt S, Gosheger G, Theil C, Schneider KN. An ergonomic golf grip leads to lower forearm muscle activity. BMC Musculoskelet Disord. 2024;25(1):668. PMID 39187838.
20. Grieß D, Schneider KN, Gosheger G, Theil C, Bochnia JM, Bockholt S. Graphite shafts reduce forearm muscle activity in golf. BMC Musculoskelet Disord. 2026;27:175. PMID 41673660.
21. Budney DR. Measuring grip pressure during the golf swing. Res Q. 1979;50(2):272-277. PMID 472468.
