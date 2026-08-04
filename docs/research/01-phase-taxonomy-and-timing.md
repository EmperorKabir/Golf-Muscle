# T-011a — Golf Swing Phase Taxonomy and Timing

Research basis for the app's swing timeline (address → follow-through slider), used to place
phase boundaries and drive the muscle-activation animation. Compiled from four parallel
cross-referenced research passes (WebSearch, many independent sources). Every numeric/definitional
claim is cited. Disagreements are stated as ranges, not resolved by picking a side. Items that
could not be verified against a primary source are flagged explicitly — do not treat them as fact
in the app without further sourcing.

**Session constraint:** the WebSearch budget (200 calls) was shared and exhausted across the four
research passes. Several planned verification searches were cut short; each gap is flagged inline
rather than filled with an unsourced number.

---

## 1. Standard phase divisions in the biomechanics/EMG literature

### 1.1 The Centinela/Jobe–Pink–Perry lineage (the de facto EMG standard)

- Foundational paper: Jobe FW, Moynes DR, Antonelli DJ (1986). "Rotator Cuff Function During a
  Golf Swing." *Am J Sports Med* 14(5):388–392. Indwelling EMG (8 shoulder muscles) synchronised
  to 450 fps film. Secondary sources state the swing was broken into **four segments** for
  synchronisation, but the exact segment names could not be recovered from accessible text —
  **unverified**.
- The **canonical five-phase model**, used consistently across this research group's later shoulder,
  scapular and trunk papers:
  1. **Takeaway** — address → end of backswing (spans the *entire* backswing in this scheme).
  2. **Forward swing** — end of backswing (top) → club shaft horizontal/parallel to ground in the
     downswing.
  3. **Acceleration** — club parallel (downswing) → ball contact/impact.
  4. **Early follow-through** — impact → club horizontal/parallel to ground in follow-through.
  5. **Late follow-through** — club parallel (follow-through) → end of swing (finish).
  - Sources: McHardy A, Pollard H, "Lower back pain in golfers: A review," *J Chiro Med* 2005;
    McHardy A, Pollard H, Luo K, "Golf injuries: A review," *Sports Med* 2005 (both as cited via a
    golf-injury review, https://pmc.ncbi.nlm.nih.gov/articles/PMC1175860/ — the review's own
    author/title not independently confirmed, flagged); corroborated independently by a second,
    separate synthesis giving identical names/boundaries.
  - This is the scheme under which the primary %MVC muscle-activation numbers in the classic
    literature were collected and reported, making it the most defensible backbone for an
    EMG-driven app.
- Papers using this five-phase scheme across body regions:
  - Shoulder: Pink M, Jobe FW, Perry J (1990). "Electromyographic analysis of the shoulder during
    the golf swing." *Am J Sports Med* 18(2):137–140. PubMed 2343980.
    https://journals.sagepub.com/doi/10.1177/036354659001800205
  - Scapula: **Kao JT, Pink M, Jobe FW, Perry J (1995). "Electromyographic analysis of the scapular
    muscles during a golf swing." *Am J Sports Med* 23:19–23.** https://pubmed.ncbi.nlm.nih.gov/7726345/
    — **correction to a common assumption:** this is a scapular-muscle study, not an elbow study.
  - Hip/knee: **Bechler JR, Jobe FW, Pink M, Perry J, Ruwe PA (1995). "Electromyographic analysis of
    the hip and knee during the golf swing."** *Clin J Sport Med* 5:162–166 (full citation recovered
    only via secondary synthesis, primary text not independently confirmed — flagged). — **correction:**
    this is a hip/knee study, not a shoulder study.
  - Trunk: Pink M, Perry J, Jobe FW (1993). "Electromyographic analysis of the trunk in golfers."
    *Am J Sports Med* 21(3). https://journals.sagepub.com/doi/abs/10.1177/036354659302100310. Reported
    finding: all trunk muscles show low activity (<30% of maximal muscle test) during takeaway and
    higher, sustained activity (>30%) through the rest of the swing.

### 1.2 Expanded 7–8-panel schematic (same scheme, finer backswing resolution — not a rival taxonomy)

- A widely reproduced figure captioned "Phases of the golf swing" appears near-identically in at
  least two sources:
  https://www.researchgate.net/figure/Phases-of-the-golf-swing-A-Address-position-B-early-back-swing-C-late-back_fig1_7522778
  and
  https://www.researchgate.net/figure/The-phases-of-the-golf-swing-A-Address-position-B-Early-backswing-C-Top-of_fig1_26736067
- Sequence: **(A) Address → (B) Early backswing → (C) Late backswing → (D) Top of swing →
  (E) Downswing → (F) Acceleration → (G) Early follow-through → (H) Late follow-through.**
- This is the same 5-phase EMG model with "Takeaway" subdivided into early/late backswing/top, plus
  an explicit address panel — not a competing scheme, but shows backswing resolution varies by
  paper. **Provenance of the original figure (which primary paper it was first drawn for) is
  unverified** — it appears to be reproduced/adapted across review articles.

### 1.3 Coarser 4-phase kinematics consensus (general biomechanics, not EMG-specific)

- Bourgain M, et al. (2022). "Golf Swing Biomechanics: A Systematic Review and Methodological
  Recommendations for Kinematics." *Sports* 10(6):91 (MDPI). https://www.mdpi.com/2075-4663/10/6/91 ;
  PMC: https://pmc.ncbi.nlm.nih.gov/articles/PMC9227529/. Reviewed 92 kinematics articles.
  Full text was blocked (HTTP 403) on both MDPI and PMC during research, so the following is a
  **secondary-source synthesis, not independently confirmed from primary text**: *"There is a
  consensus in the definition of movement, with four main phases (address, backswing, downswing,
  and follow-through)."*
- **This is a genuine granularity disagreement, not mere terminology**: general kinematics papers
  commonly use 4 broad phases; EMG papers commonly use the finer 5-phase (or 7–8-panel) scheme.

### 1.4 Coaching "P-System" (P1–P10) — a separate, non-EMG lineage

- A ten-position system used in golf instruction/swing-analysis software (e.g. HackMotion,
  https://hackmotion.com/golf-swing-positions/):
  P1 Address — P2 Takeaway (club parallel to ground) — P3 Halfway back (lead arm parallel to
  ground) — P4 Top of backswing (club ~parallel to ground) — P5 Early downswing (top → club
  parallel) — P6 Pre-impact (shaft parallel, pre-impact) — P7 Impact — P8 Release (post-impact) —
  P9 Finish (lead arm parallel, mirror of P3) — P10 End of swing (balanced, facing target).
- **Creator, origin and first-publication date not identified — unverified provenance.** This is a
  coaching/commercial-software taxonomy, not a peer-reviewed EMG research scheme. Useful for
  cross-referencing landmark names (see §5) but not equal-weight to the Jobe/Pink/Perry standard for
  driving the app's %MVC-based activation curve.

### 1.5 Summary of disagreement

- Phase count ranges from **4** (general kinematics consensus per Bourgain 2022) to **5**
  (EMG-literature standard) to **7–8** (expanded schematic subdividing the backswing) to **10**
  (coaching P-system, non-EMG).
- **Recommendation for the app:** anchor the muscle-activation timeline to the 5-phase
  Centinela/Jobe-Pink-Perry scheme, since that is the scheme the underlying %MVC data (T-011b–d)
  was collected under. Use the P-system/expanded-schematic landmark names only as finer sub-markers
  within those 5 phases (see §5), not as an alternative source of truth.

---

## 2. Typical phase durations (milliseconds)

**Every duration figure below is driver-based or club-unspecified.** No study was found reporting
iron-specific (let alone 8-iron-specific) phase durations — flagged as a genuine data gap for this
app's stated 8-iron use case (see §2.6).

### 2.1 Backswing duration (address → top)

| Source | Population | Value |
|---|---|---|
| Cheetham, TPI 3D database, "Measuring the Timing of the Golf Swing from Video" (mytpi.com) | Tour pro, driver | mean **847 ms**, SD 111 ms (≈736–958 ms); "fast" example 750 ms, "slow" example 900 ms |
| Grober RD (2006), "Towards a Biomechanical Understanding of Tempo in the Golf Swing," arXiv:physics/0611291 | Professional-level | **731 ± 21 ms** |

- Grober's figure is a physics preprint; peer-reviewed publication status could not be confirmed
  this session — treat as preprint-tier. Its numbers come from consistent search-engine synthesis,
  not a direct read of the PDF (text was not extractable) — moderately-but-not-fully verified.

### 2.2 Downswing duration (top → impact)

| Source | Population | Value |
|---|---|---|
| Cheetham, TPI | Tour pro, driver | **233–296 ms** (fast example 250 ms, slow example 300 ms) |
| Grober (2006) | Professional-level | **258 ± 8 ms** |
| Bourgain et al. (2022), *Sports* 10(6):91 (via secondary synthesis, not independently confirmed — publisher pages blocked) | Recreational (hcp >5), driver | **0.25 ± 0.02 s** |
| Same review | Highly-skilled amateur (hcp <5) + professional, driver | **0.31 ± 0.04 s** — i.e. *longer*, not shorter, for the more skilled group |
| US Patent 8,342,978 background section (not peer-reviewed, low reliability) | Pro / advanced amateur / recreational | ≈0.26 s / ≈0.34 s / ≈0.42 s — shortens with skill (opposite direction to the Bourgain figure) |

- **Consensus range for skilled/tour golfers: roughly 230–300 ms**, extending toward 400+ ms for
  slower/weaker swings.
- **Genuine, unresolved literature disagreement:** the Bourgain (2022) review reports *more* skilled
  golfers taking *longer* to complete the downswing than recreational golfers, while the patent
  background source (low reliability) claims the opposite (skill shortens downswing time). Do not
  silently resolve this — state both.
- One additional figure (elderly amateur, hcp≈25, downswing 433±18 ms) surfaced with **no traceable
  source** — do not use.

### 2.3 Backswing : downswing ratio

- TPI 3D database (large tour sample): **3.2:1** (single example golfer 3.3:1). — Cheetham, TPI.
- Grober (2006): **2.8:1**, described in the source as "very nearly" 3:1.
- Popular-instruction range cited alongside these: **2.8:1 to 3.2:1** for elite players regardless of
  absolute swing speed.
- This is one of the more robust figures in the dataset: an independent physics preprint and a
  commercial 3D-motion database converge on ≈3:1 despite unrelated methodologies.

### 2.4 Tempo ratio — popular instruction vs peer-reviewed, explicitly separated

- **Popular-instruction (not peer-reviewed):** John Novosel, *Tour Tempo* (tourtempo.com). Proposes
  a constant 3:1 backswing:downswing ratio in 30fps-frame pairs: 27:9 (≈900:300 ms, e.g. Tiger Woods
  1997 Masters), 24:8 (≈800:267 ms, e.g. Ernie Els), 21:7 (≈700:233 ms), 18:6 (≈600:200 ms, cited for
  faster-tempo modern players e.g. Rickie Fowler). Source:
  tourtempo.com/blogs/tips/what-the-numbers-mean.
- **Academic/physics (preprint, publication status unconfirmed):** Grober (2006), arXiv:physics/0611291
  — models the ≈3:1 (measured 2.8:1) ratio as emergent from the body/club system behaving as a simple
  harmonic oscillator ("biomechanical clock").
- These two lineages are methodologically unrelated but numerically convergent (~3:1) — do not cite
  them as a single confirmed academic consensus; they are independent corroboration at best.

### 2.5 Transition ("pause" at top of backswing)

- **No peer-reviewed source reports a discrete transition-phase duration in milliseconds.** The
  biomechanics literature treats "top of backswing" as an instantaneous kinematic landmark (club/
  segment angular velocity crossing zero), not a phase with its own measured duration.
- Instructional sources (hackmotion.com; practical-golf.com; a golf.com interview with biomechanist
  Dr Sasho Mackenzie) discuss a subjective "pause" as a coaching cue but supply **no quantified
  duration** (Mackenzie is quoted only qualitatively: "a longer pause may cost a few mph but can
  improve coordination").
- **App guidance: model the transition as ~0 ms / an instantaneous zero-velocity event**, not as a
  phase with an assigned duration, unless a better source is found later.

### 2.6 Downswing sub-phases (early vs late / forward-swing vs acceleration)

- The Pink/Jobe/Perry scheme's Phase 2 (Forward swing: top → club horizontal) and Phase 3
  (Acceleration: club horizontal → impact) are **landmark-defined, not time-defined** — no source
  gives a millisecond or percentage split between them. If the app needs a numeric split, it must be
  derived from kinematic-sequence timing data (§3), not from a directly reported duration split.

### 2.7 Follow-through duration (impact → finish)

- Cheetham, TPI 3D database: tour pro driver, **525–825 ms** (single example golfer 433 ms, "a fast
  finish"). This is the **only sourced follow-through figure found**; no peer-reviewed EMG/biomechanics
  paper with a follow-through-duration figure was located. Follow-through is comparatively
  under-studied (less consequential to ball flight, harder to define a clean endpoint).
- No iron-specific or skill-stratified follow-through data found.

### 2.8 Total swing duration (address → finish)

- **No single source reports one aggregate total-swing-time figure.** A purely arithmetic sum of the
  TPI figures above (847 ms backswing + ~265 ms downswing + ~675 ms follow-through midpoint) gives
  roughly **1.6–1.9 s address-to-finish for a tour-pro driver swing** — this is a **derived estimate,
  not a cited figure**; label it as such if used in-app, never as sourced data.

### 2.9 Iron vs driver — explicit gap

- Every duration figure above is either explicitly driver-based or club-unspecified. **No study was
  found reporting backswing/downswing/follow-through timing specifically for an iron**, and none for
  an 8-iron. No verifiable scaling factor (peer-reviewed or instructional) for how much faster/shorter
  an iron swing's timing is versus driver was found. **Flag to product owner:** iron-specific timing
  for the app's stated 8-iron use case will need either (a) an approximation from driver data with an
  explicitly labelled, unverified scaling assumption, or (b) a targeted follow-up literature search
  not completed in this pass.

---

## 3. Kinematic sequence

### 3.1 Definition and the proximal-to-distal principle

- The kinematic sequence is the proximal-to-distal ordering of peak segmental angular velocities
  during the downswing: **pelvis → thorax (upper torso) → lead arm → club**, each segment
  accelerating, peaking, then decelerating to hand off energy to the next link. Sources: TPI, "The
  Linear Kinematic Sequence," mytpi.com; interview with Dr Phil Cheetham, golfwell.co
  (both secondary/industry sources for the qualitative description).
- Deceleration is reported to follow the same order — pelvis decelerates first, then chest, then
  arms, then club — which is believed to be the mechanism of energy transfer up the chain
  (athletesuntapped.com — coaching/secondary source, qualitative only).
- Stated across coaching sources as near-universal among tour professionals ("virtually every
  professional golfer on tour ... has the exact same kinematic sequence": pelvis, torso, lead arm,
  club) — this is an industry-consensus statement, not a peer-reviewed statistic; treat accordingly.

### 3.2 Peak angular velocity magnitudes

- **Nesbit SM (2005). "A Three-Dimensional Kinematic and Kinetic Study of the Golf Swing." *J Sports
  Sci Med* 4(4):499–519.** https://www.jssm.org/volume04/iss4/cap/jssm-04-499.pdf ;
  https://pmc.ncbi.nlm.nih.gov/articles/PMC3899667/. Sample: 84 male + 1 female amateurs, hcp 0–20,
  mean hcp 5.8. Reports **club** (not body-segment) angular velocity: maximum primary swing-plane
  ("alpha") angular velocity averaged **1,756.25°/s** (range ~1,600–1,910°/s across subjects), peaking
  on average 0.025 s before impact for a scratch golfer (range −0.020 s to +0.010 s relative to
  impact across other subjects). At impact: pitch ("beta") velocity averaged −145°/s, roll ("gamma")
  velocity averaged −925°/s. **These are club-only Euler-angle components — do not conflate with
  body-segment (pelvis/thorax/arm) values below.**
- **Meister DW, Ladd AL, Butler EE, Zhao B, Rogers AP, Ray CJ, Rose J (2011). "Rotational Biomechanics
  of the Elite Golf Swing: Benchmarks for Amateurs." *J Appl Biomech* 27(3):242–251.** PubMed
  21844613. Sample: 10 professional + 5 amateur male golfers. Measured upper-torso rotation, pelvic
  rotation, X-factor, O-factor (pelvic obliquity), S-factor (shoulder obliquity), normalised free
  moment. Among professionals, peak free moment/kg, peak X-factor and peak S-factor were highly
  consistent (coefficients of variation 6.8%, 7.4%, 8.4–8.8%). Four variables correlated strongly with
  impact clubhead speed: free moment/kg, X-factor at impact, peak X-factor, peak upper-torso rotation
  (median r = 0.943, 0.943, 0.900, 0.900 respectively). Key finding: **downswing was initiated by
  reversal of pelvic rotation, followed by reversal of upper-torso rotation** in professionals —
  the proximal segment reverses toward the target before the distal segment, consistent with
  proximal-to-distal sequencing.
- A pelvis/thorax/lead-arm/forearm/hand peak-velocity dataset (480/605/1310/1490/1650 °/s) surfaced
  during research but its **primary study could not be identified — flagged unverified, do not use**.
- A figure of "maximum pelvis angular velocity 91.5°/s" surfaced but **contradicts the ~300–500°/s
  range reported elsewhere and could not be corroborated — flagged unreliable, do not use** (likely a
  unit or transcription error in its source page).

### 3.3 Timing offsets between segment peaks

- Only qualitative/relative claims were verifiable: each distal segment reaches peak angular velocity
  after its proximal driver, and "there is a larger interval between the arm peak and the club peak —
  more than twice as long as from the hip to arm peak" (search-engine synthesis; **underlying primary
  study not identified — flagged unverified for exact millisecond values**).
- **Cheetham PJ, Martin PE, Mottram RE, St Laurent BF (2001). "The Importance of Stretching the
  X-Factor in the Downswing of Golf: The X-Factor Stretch."**
  https://www.philcheetham.com/wp-content/uploads/2011/11/Stretching-the-X-Factor-Paper.pdf — found
  pelvis-thorax angular separation continues to increase briefly into early downswing as the pelvis
  begins rotating toward the target slightly before the thorax (a proximal-lead timing gap at
  downswing onset), but **no exact millisecond value for this specific lag** was extractable (PDF text
  extraction was degraded in this session).
- **No dataset giving actual millisecond offsets between pelvis/thorax/arm/club peaks was found** —
  this is an open gap; only ordering, not timing gaps, is well established from accessible sources.

### 3.4 Amateur vs professional sequencing differences

- Recreational/amateur golfers "tend to use their arms earlier in the downswing, have poorer
  coordination, weaker power production, and inefficient energy transfer from segment to segment when
  compared with elites" (search synthesis referencing Meister et al. 2011 context) — linked in
  coaching literature to increased upper-extremity injury risk.
- Common amateur fault named in applied-biomechanics/coaching sources: arms and/or torso firing before
  the lower body ("early release"/"over the top"), producing slices, pulls, reduced clubhead speed
  (athletesuntapped.com — coaching source, not peer-reviewed).
- **Zheng N, Barrentine SW, Fleisig GS, Andrews JR (2008). "Kinematic Analysis of Swing in Pro and
  Amateur Golfers." *Int J Sports Med.*** https://www.thieme-connect.de/products/ejournals/pdf/10.1055/s-2007-989229.pdf
  — optoelectronic system, 240 Hz; 18 professional + 18 low-hcp + 18 mid-hcp + 18 high-hcp golfers
  (n=72); 10 displacement parameters at address, top of backswing, ball contact. Statistically
  significant kinematic differences were found **only between the two extreme groups** (professional
  vs high-handicap), not between adjacent skill tiers. Related finding from the same lineage
  (PubMed 18563677, "Swing Kinematics for Male and Female Pro Golfers"): LPGA players showed lower
  maximum wrist velocities, lower left-wrist-extension velocity, and lower clubhead velocity than PGA
  players.
- **Not verified:** a specific percentage of amateurs achieving the full "ideal" proximal-to-distal
  sequential pattern. No source located gave a quantified percentage — treat this as an open gap; do
  not state a percentage in the app without further sourcing.

---

## 4. X-factor and X-factor stretch

### 4.1 Definitions and origin

- **X-factor**: angular separation (differential rotation) between shoulders/thorax and pelvis/hips in
  the transverse plane, conventionally measured at top of backswing. Example given across sources:
  90° shoulder turn − 50° hip turn = 40° X-factor (mytpi.com).
- **Peer-reviewed originating source:** McTeigue M, Lamb SR, Mottram R, Pirozzolo F (1994). "Spine and
  hip motion analysis during the golf swing." In *Science and Golf II: Proceedings of the World
  Scientific Congress of Golf*, pp. 50–58, E&FN Spon, London. Studied 51 PGA Tour + 46 Senior PGA Tour
  pros; found long hitters generated more spinal coil (X-factor) than others, but **found no strong
  evidence that X-factor magnitude at the top discriminates amateur from professional skill level in
  general**. Full text is conference-proceedings-only and was not independently accessible this
  session — phase-boundary/exact-value details from it are unverified beyond what secondary sources
  report.
- **Popular-instruction source:** Jim McLean popularised "X-Factor" in 1992 *Golf Magazine* articles
  (later *The X-Factor Swing*, with John Andrisani, 1997, HarperCollins). McLean's analysis (5
  long-hitting vs 5 short-hitting tour pros): **long hitters averaged 38° X-factor vs 24° for short
  hitters** — a popular-press finding, not peer-reviewed.
- **X-factor stretch**: the further transient *increase* in X-factor in early downswing, as the pelvis
  begins rotating toward the target while the thorax/shoulders remain rotated back, before the
  separation decreases again through impact. Named in Cheetham PJ, Martin PE, Mottram RE, St Laurent
  BF, "The importance of stretching the 'X-Factor' in the downswing of golf: The 'X-Factor Stretch.'"
  **Publication year is disputed across sources: cited as 2001 in several secondary sources, but the
  directly-fetched PDF is labelled with 2008 authorship ordering (St Laurent, Cheetham, Mottram) —
  flagged, unresolved.** https://www.philcheetham.com/wp-content/uploads/2011/11/Stretching-the-X-Factor-Paper.pdf

### 4.2 Magnitude at top of backswing — cross-study comparison (substantial disagreement)

| Source | Population | X-factor at top |
|---|---|---|
| Cheetham et al. 2001/2008 PDF | Skilled golfers | ~90° (extraction uncertain, see caveat below) |
| Zheng, Barrentine, Fleisig, Andrews (2008), *Int J Sports Med* 29(12):965–70 | LPGA (n=25) / PGA (n=25) | **58° men, 60° women** |
| McLean 1992 (popular press) | 5 long-drive vs 5 short-drive tour pros | **38° vs 24°** |
| TPI (proprietary tour-average, no formal citation) | "Tour average" | **~42°** |
| Meister et al. (2011), *J Appl Biomech* 27(3):242–251 | 10 pro + 5 amateur | Peak X-factor and X-factor-at-impact strongly correlated with clubhead speed (median r ≈0.90–0.943); absolute degree values by group not confirmed in extraction |
| McTeigue et al. 1994 | 51 PGA + 46 Senior PGA pros | No single mean recovered; found long hitters have more coil but **no significant skill-level discrimination** by X-factor alone |

- Reported top-of-backswing X-factor spans roughly **24°–90°** depending on study — and critically, on
  **measurement method** (2D vs 3D, marker placement, raw angle-difference vs plane-projection).
- **Brown K, Selbie WS, Wallace ES. "The X-Factor: an evaluation of common methods used to analyse
  major inter-segment kinematics during the golf swing." *J Sports Sci*** (year cited as ~2013 in
  secondary sources, **not independently confirmed — flagged**) explicitly concludes **there is no
  consistent method within the golf-biomechanics literature for calculating X-factor**, which is the
  primary reason absolute magnitudes vary so widely across studies.
  https://www.researchgate.net/publication/235883466_The_X-Factor_An_evaluation_of_common_methods_used_to_analyse_major_inter-segment_kinematics_during_the_golf_swing
- **On skill-level discrimination — findings directly conflict:** McTeigue (1994) and a Cheetham et al.
  2001 reanalysis (per a secondary literature review) found no significant X-factor difference between
  professionals and amateurs; a source citing Hellström (2009, **primary paper not verified, flagged**)
  likewise reported no significant ball-flight difference with increased X-factor. Other secondary
  summaries claim professionals show greater separation than amateurs, but the clearest related
  finding (Myers et al. 2008, below) is actually about separation *velocity*, not static magnitude.
  **Net assessment: X-factor magnitude alone is not a reliably replicated skill discriminator in this
  literature** — the null result is one of the more consistently repeated findings.

### 4.3 Related but distinct: torso-pelvis separation velocity (Myers et al. 2008)

- Myers J, Lephart S, Tsai Y-S, Sell T, Smoliga J, Jolly J (2008). "The role of upper torso and pelvis
  rotation in driving performance during the golf swing." *J Sports Sci* 26(2):181–188. PubMed
  17852693. n=100 recreational golfers, own driver, launch-monitor ball velocity. Finding:
  torso-pelvic separation contributes to greater upper-torso rotation *velocity* and torso-pelvic
  separation *velocity* during downswing, which contributes to greater ball velocity. **This is a
  velocity/kinematic-sequence finding, distinct from static X-factor-degree values — do not conflate.**

### 4.4 X-factor stretch — magnitude and timing

- Cheetham et al. PDF: skilled golfers stretch to **~73.5° during downswing, an increase of ~13.4°**
  beyond the top-of-backswing X-factor (this source's own top-of-backswing baseline, ~90°, is notably
  higher than Zheng et al.'s 58–60°, reinforcing the Brown/Selbie/Wallace point that measurement
  convention drives much of the cross-study spread).
- Related/same lineage, reported elsewhere: skilled golfers increased X-factor by **19%** at downswing
  initiation vs **13%** for less-skilled golfers (statistically significant), while the *raw*
  X-factor-magnitude difference between skill groups was only **~11% and not statistically
  significant** — i.e. X-factor *stretch* differentiated skill level where static X-factor did not.
- Timing: peak X-factor stretch reported at **~20 ms after downswing initiation** for low-handicap
  golfers — **moderate confidence only**; the primary paper's exact figure was not independently
  confirmed from the PDF extraction.
- TPI proprietary tour-average (non-peer-reviewed): X-factor **≈42°** at top, stretch adds **≈5°** in
  early downswing — far smaller than Cheetham's ~13.4°, again reflecting differing conventions/
  populations.
- Mechanistic rationale (multiple sources): the pelvis rotates toward the target while shoulders/
  thorax momentarily stay back, stretching trunk musculature and eliciting a stretch-shortening/
  stretch-reflex effect hypothesised to increase force output and elastic energy return.
- **Adjacent, easily confused metric:** "crunch factor" = trunk lateral-bend angle × axial rotation
  velocity of torso relative to pelvis, maximised around impact/early follow-through — a spinal-loading
  metric associated with low-back injury risk, **not** the same as X-factor stretch.
  https://www.sciencedirect.com/science/article/abs/pii/S1529943013015593

### 4.5 Skill-tier granularity — data gap

- No reliably sourced **three-tier** (tour pro / low-handicap amateur / high-handicap amateur)
  X-factor or X-factor-stretch dataset with specific degree values was found. Available comparisons
  are binary (skilled vs less-skilled, or pro vs amateur) at best. **Flag as an open item** if the app
  needs finer skill-tier granularity for this metric.

### 4.6 Clubhead-speed correlation — a genuinely contested area (state both sides)

**Supporting a strong relationship:**
- Meister et al. (2011): peak X-factor and X-factor-at-impact showed median r ≈ 0.900–0.943 with
  clubhead speed; peak free moment/kg ≈0.943.
- **Joyce C (2017). "The most important 'factor' in producing clubhead speed in golf." *Hum Mov Sci*
  55:138–144.** PubMed 28822263. n=15 low-handicap male golfers, 10-camera 250 Hz mocap, own driver +
  5-iron. Found **lower-trunk X-factor stretch strongly correlated with clubhead speed for the 5-iron
  (r = 0.78, p < 0.01)**; four X-factor-family variables moderately-to-strongly correlated with
  clubhead speed for the 5-iron. **Critically, no significant correlation was found for the driver** —
  club-dependent result, directly relevant to this app's 8-iron use case (positive supporting evidence
  exists specifically for irons, not confirmed for driver).

**Challenging or complicating the relationship:**
- Brown, Selbie, Wallace (~2013): methodological critique — X-factor/stretch values are not comparable
  across studies given the lack of a standardised calculation method, undermining pooled or
  cross-study performance claims.
- A secondary literature review (citing Hellström 2009, unverified primary) reports no significant
  ball-displacement difference associated with increased X-factor, and no significant separation-angle
  difference between professionals and amateurs in some reanalyses of Cheetham et al. 2001.
- Joyce (2017) is double-edged: often cited as supporting evidence, but its driver-null/iron-positive
  split is itself evidence against a simple universal "more stretch = more speed" rule — the
  relationship appears **club-specific**, not a fixed law.
- A general caution recurring across secondary sources — "delaying wrist release or increasing
  X-factor stretch does not guarantee increased clubhead speed" — could not be pinned to one primary
  source; flagged.

**Net position:** X-factor stretch as a descriptive/mechanistic concept (pelvis leading, transient
separation increase, stretch-shortening cycle) is well established. Its **magnitude is
measurement-convention-dependent** (5°–13.4°+ depending on method/population). Its **correlation with
clubhead speed is positive in several studies (r up to 0.78–0.94) but not universal** — it varies by
club (iron vs driver — notably supportive for iron, the app's actual use case) and by measurement
method. Treat "X-factor stretch increases clubhead speed" as **supported but not settled**, not
established fact.

---

## 5. Key kinematic landmarks used to time/segment the swing

- **Club parallel to ground in backswing**: not a named boundary in the strict 5-phase Jobe/Pink/Perry
  scheme (their "Takeaway" spans the whole backswing) — it is a finer-grained checkpoint used in later,
  more subdivided taxonomies (§1.2, §1.4), roughly corresponding to "P2" in the modern P-system, near
  the takeaway/early-backswing boundary.
- **Top of backswing**: two coexisting operational definitions coexist in the literature:
  - **Kinematic**: the instant club (or segment) angular velocity crosses zero — the point where
    velocity/direction reverses from backswing-directed to downswing-directed, and acceleration flips
    from negative to positive. Attribution to one specific primary paper could not be pinned down this
    session — the *existence* of this definition is verified via cross-referenced methodology
    discussions, but not tied to a single named study.
  - **Visual/positional**: club shaft visually parallel to ground / at its highest point — the more
    common instructional/P-system definition.
  - **No source quantified the typical discrepancy** between these two definitions when they diverge.
- **Club parallel to ground in downswing**: confirmed as the Forward-swing→Acceleration boundary in the
  Jobe/Pink/Perry 5-phase scheme (§1.1).
- **Lead arm horizontal**: confirmed as a *distinct* landmark from club-parallel in the modern P-system
  (P3 = lead arm parallel in backswing; P5-adjacent = lead arm reaching parallel in downswing) —
  hackmotion.com. **Important caveat: the P-system is a later/parallel instructional taxonomy, not
  verified as originating in the Jobe/Pink/Perry 1990/1993 papers themselves.** Whether "lead arm
  horizontal" was literally used as a named landmark in those original papers could not be confirmed
  (their full text was not accessible) — well-attested only in later/modern sources. Do not present it
  as an original Jobe/Pink/Perry landmark without further verification.
- **Impact**: detection method varies by study, itself a source of cross-study timing disagreement:
  - Video-frame coding of six discrete instants (address, end of backswing, mid-downswing, ball
    impact, mid-follow-through, end of follow-through) — underlying study not individually identified,
    attribution unverified.
  - Force-plate + EMG synchronisation with high-speed video for displacement (ScienceDirect, "Determine
    an effective golf swing by swing speed and impact precision tests" — full citation not pinned down).
  - Acoustic/microphone-triggered synchronisation: impact sound triggers LEDs visible to all cameras
    plus a synchronisation voltage pulse to EMG/force-plate A/D converters for frame-accurate alignment
    — specific paper not identified by name this session, attribution unverified.
- **Club parallel in follow-through**: confirmed as the Early-follow-through→Late-follow-through
  boundary in the Jobe/Pink/Perry scheme (symmetric counterpart to the downswing club-parallel
  landmark). The modern P-system's nearest equivalent (P9/finish) is defined by lead-arm-parallel on
  the lead side rather than explicitly "club parallel" — a minor terminological divergence between the
  academic symmetric-landmark convention and the modern P-system's own checkpoints.

**Disagreement/taxonomy note:** the task brief's framing that "lead arm horizontal" is used
"especially in Jobe/Pink/Perry-lineage phase definitions" could not be directly confirmed against the
primary 1990/1993 papers — that specific landmark is well-attested only in the later/modern
instructional literature (P-system). The fine-grained landmark checkpoints (club-parallel-in-backswing,
lead-arm-horizontal) belong to a later or parallel elaboration of the same underlying swing, not
verified as originating in the original Jobe/Pink/Perry papers — treat as complementary, not
interchangeable, taxonomies.

---

## 6. EMG timeline normalisation convention

- **No single universal convention exists** — this is itself a documented methodological
  inconsistency in the literature, not a settled standard. Design the app's internal representation
  to be convention-agnostic (store absolute time per phase, derive % on demand) given this.
- **Absolute time (ms/seconds), keyed to the 5 named phases**, is the convention used by the classic
  Jobe/Pink/Perry/Kao EMG series — they report phase-by-phase %MVC values, not a continuous 0–100%
  curve.
- **Percentage-of-swing-cycle normalisation** appears in more recent kinematic/kinetic (non-classic-EMG)
  papers, for cross-subject comparability given variable swing durations.
- One claim surfaced but **could not be confirmed against a primary paper — unverified, treat with
  caution**: a study normalising swing time as beginning-of-backswing = 0%, ball impact = 100%,
  end-of-follow-through = 140% (follow-through end defined by local minimum of vertical clubhead
  displacement). Plausible and analogous to gait-cycle % normalisation, but not independently verified.
- **Verikas A, Vaiciukynas E, Gelzinis A, Parker J, Olsson MC (2016). "Electromyographic Patterns
  during Golf Swing: Activation Sequence Profiling and Prediction of Shot Effectiveness." *Sensors*
  16(4):592.** https://pmc.ncbi.nlm.nih.gov/articles/PMC4851105/ — explicitly does **not** normalise to
  a 0–100% whole-swing cycle. Uses absolute time (total swing time range **1.5–2.2 s** across subjects
  — start/end reference points relative to "address" not fully specified, possibly includes a
  pre-swing capture window, flagged as ambiguous) and defines phase-relative peak timing as position
  within each individual segment's own duration (i.e. phase-relative normalisation, not whole-swing
  normalisation).
- A duration-ratio claim relevant to anchoring a 0–100% scale (coaching/technology sources, **not
  confirmed peer-reviewed — lower confidence**): professional players' time split from swing start to
  impact is commonly cited as **~75% backswing / 25% downswing**, vs **~70%/30%** for amateurs. Note
  this is an address-to-*impact* normalisation base; an address-to-*finish* 0–100% scale would place
  top-of-backswing much earlier (~25–30%) — **which endpoint anchors 100% (impact vs finish) is
  critical and appears to vary by paper; no single dominant convention could be confirmed.**
- **No confirmed instance found of a gait-analysis-style decile/percentile inter-subject
  time-normalisation protocol** (e.g. resampling each subject's swing to a fixed N frames before
  averaging) specifically in golf-EMG literature — search was cut short by budget exhaustion before
  this could be confirmed or ruled out. **Flagged as an open gap** for a future targeted search
  (suggested terms: "time-normalized golf EMG ensemble average," "golf swing EMG interpolated 101
  points").

---

## Consolidated recommendations for the app's timeline model

- Use the **5-phase Jobe/Pink/Perry/Kao scheme** (Takeaway, Forward swing, Acceleration, Early
  follow-through, Late follow-through) as the backbone, since that is the scheme the %MVC data was
  collected under (relevant to T-011b–d).
- Use the **club-parallel / lead-arm-horizontal / top-of-backswing (zero-velocity)** landmarks from
  §5 as finer sub-markers inside those 5 phases where useful for animation keyframing, clearly
  distinguishing academic-lineage landmarks from P-system landmarks in code/comments if both are used.
- For phase durations, default to the **driver-based tour-pro figures** in §2 (backswing ≈730–850 ms,
  downswing ≈230–300 ms, ≈3:1 ratio, follow-through ≈525–825 ms) as a *starting* skeleton, but flag in
  the app's data model that these are not iron-specific — apply and clearly label any provisional
  scaling assumption if 8-iron timing is approximated from driver data before better data is sourced.
- Do not implement a fixed-duration "transition pause" — treat top of backswing as instantaneous.
- Do not use any of the individually-flagged "unverified" numeric values (pelvis 91.5°/s; the
  480/605/1310/1490/1650°/s segment set; the 0/100/140% normalisation claim; the amateur-sequencing
  percentage) without a follow-up verification pass.

---

## Master source list (deduplicated)

1. Jobe FW, Moynes DR, Antonelli DJ (1986). "Rotator Cuff Function During a Golf Swing." *Am J Sports
   Med* 14(5):388–392. https://journals.sagepub.com/doi/abs/10.1177/036354658601400509
2. Pink M, Jobe FW, Perry J (1990). "Electromyographic analysis of the shoulder during the golf
   swing." *Am J Sports Med* 18(2):137–140. PubMed 2343980.
   https://journals.sagepub.com/doi/10.1177/036354659001800205
3. Pink M, Perry J, Jobe FW (1993). "Electromyographic analysis of the trunk in golfers." *Am J
   Sports Med* 21(3). https://journals.sagepub.com/doi/abs/10.1177/036354659302100310
4. Kao JT, Pink M, Jobe FW, Perry J (1995). "Electromyographic analysis of the scapular muscles
   during a golf swing." *Am J Sports Med* 23:19–23. https://pubmed.ncbi.nlm.nih.gov/7726345/
5. Bechler JR, Jobe FW, Pink M, Perry J, Ruwe PA (1995). "Electromyographic analysis of the hip and
   knee during the golf swing." *Clin J Sport Med* 5:162–166. (Full text not independently accessed;
   citation via secondary synthesis.)
6. McTeigue M, Lamb SR, Mottram R, Pirozzolo F (1994). "Spine and hip motion analysis during the golf
   swing." *Science and Golf II: Proceedings of the World Scientific Congress of Golf*, pp. 50–58,
   E&FN Spon, London.
7. McHardy A, Pollard H (2005). "Lower back pain in golfers: A review." *J Chiro Med.*
8. McHardy A, Pollard H, Luo K (2005). "Golf injuries: A review." *Sports Med.*
9. Golf upper-limb-injury review (title/authors not independently confirmed).
   https://pmc.ncbi.nlm.nih.gov/articles/PMC1175860/
10. Marta S, Silva L, Castro MA, Pezarat-Correia P, Cabri J (2012). "Electromyography variables
    during the golf swing: a literature review." *J Electromyogr Kinesiol* 22(6):803–813.
    https://pubmed.ncbi.nlm.nih.gov/22542769/
11. Bourgain M, et al. (2022). "Golf Swing Biomechanics: A Systematic Review and Methodological
    Recommendations for Kinematics." *Sports* 10(6):91. https://www.mdpi.com/2075-4663/10/6/91
12. Verikas A, Vaiciukynas E, Gelzinis A, Parker J, Olsson MC (2016). "Electromyographic Patterns
    during Golf Swing: Activation Sequence Profiling and Prediction of Shot Effectiveness." *Sensors*
    16(4):592. https://pmc.ncbi.nlm.nih.gov/articles/PMC4851105/
13. HackMotion. "Golf Swing Positions Explained (P Classification System)."
    https://hackmotion.com/golf-swing-positions/ (coaching source)
14. Reproduced phase-schematic figures (provenance unconfirmed):
    https://www.researchgate.net/figure/Phases-of-the-golf-swing-A-Address-position-B-early-back-swing-C-late-back_fig1_7522778 ;
    https://www.researchgate.net/figure/The-phases-of-the-golf-swing-A-Address-position-B-Early-backswing-C-Top-of_fig1_26736067
15. Cheetham P, TPI. "Measuring the Timing of the Golf Swing from Video."
    https://www.mytpi.com/articles/biomechanics/measuring-the-timing-of-the-golf-swing-from-video
16. Grober RD (2006). "Towards a Biomechanical Understanding of Tempo in the Golf Swing."
    arXiv:physics/0611291. https://arxiv.org/abs/physics/0611291 (preprint status)
17. Novosel J. *Tour Tempo.* tourtempo.com/blogs/tips/what-the-numbers-mean (popular instruction)
18. US Patent 8,342,978, "Device for instructing downswing in golf swing" (background section only).
19. golf.com interview with Dr Sasho Mackenzie re: pause at top (qualitative only).
20. hackmotion.com, "Pause at the Top of the Backswing" (instructional, no numeric data).
21. practical-golf.com, "Swing Tempo" and "Golf Swing Transition" (instructional, cross-reference for
    2.8–3.2:1 ratio range).
22. Cheetham PJ, Martin PE, Mottram RE, St Laurent BF. "The Importance of Stretching the X-Factor in
    the Downswing of Golf: The X-Factor Stretch." Year disputed (2001 vs 2008 across sources).
    https://www.philcheetham.com/wp-content/uploads/2011/11/Stretching-the-X-Factor-Paper.pdf
23. Nesbit SM (2005). "A Three-Dimensional Kinematic and Kinetic Study of the Golf Swing." *J Sports
    Sci Med* 4(4):499–519. https://www.jssm.org/volume04/iss4/cap/jssm-04-499.pdf
24. Meister DW, Ladd AL, Butler EE, Zhao B, Rogers AP, Ray CJ, Rose J (2011). "Rotational Biomechanics
    of the Elite Golf Swing: Benchmarks for Amateurs." *J Appl Biomech* 27(3):242–251. PubMed
    21844613. https://journals.humankinetics.com/view/journals/jab/27/3/article-p242.xml
25. Zheng N, Barrentine SW, Fleisig GS, Andrews JR (2008). "Kinematic Analysis of Swing in Pro and
    Amateur Golfers." *Int J Sports Med.*
    https://www.thieme-connect.de/products/ejournals/pdf/10.1055/s-2007-989229.pdf
26. "Swing Kinematics for Male and Female Pro Golfers." PubMed 18563677.
    https://pubmed.ncbi.nlm.nih.gov/18563677/
27. Myers J, Lephart S, Tsai Y-S, Sell T, Smoliga J, Jolly J (2008). "The role of upper torso and
    pelvis rotation in driving performance during the golf swing." *J Sports Sci* 26(2):181–188.
    PubMed 17852693. https://exss.unc.edu/wp-content/uploads/sites/779/2013/01/Myers_jss_2008.pdf
28. Brown K, Selbie WS, Wallace ES. "The X-Factor: an evaluation of common methods used to analyse
    major inter-segment kinematics during the golf swing." *J Sports Sci* (year ~2013, unconfirmed).
    https://www.researchgate.net/publication/235883466_The_X-Factor_An_evaluation_of_common_methods_used_to_analyse_major_inter-segment_kinematics_during_the_golf_swing
- 29. Joyce C (2017). "The most important 'factor' in producing clubhead speed in golf." *Hum Mov Sci*
    55:138–144. PubMed 28822263. https://www.sciencedirect.com/science/article/abs/pii/S0167945717302063
30. McLean J (1992, *Golf Magazine* articles); McLean J & Andrisani J (1997). *The X-Factor Swing.*
    HarperCollins. (Popular-press origin of the term.)
31. TPI (Titleist Performance Institute) proprietary tour-average data (non-peer-reviewed).
    https://www.mytpi.com/articles/biomechanics/the-difference-between-x-factor-and-x-factor-stretch
32. Literature review citing Hellström (2009, primary source unverified) and a Cheetham 2001
    reanalysis. https://www.ivoryresearch.com/samples/sports-biomechanics-literature-review-the-relationship-between-the-x-factor-and-golfing-performance/
33. "The crunch factor's role in golf-related low back pain."
    https://www.sciencedirect.com/science/article/abs/pii/S1529943013015593

## Open verification gaps (flagged, not resolved — candidates for a future targeted session)

- Exact 4-segment names in Jobe, Moynes, Antonelli (1986).
- Primary-text confirmation of Bourgain et al. (2022) phase-taxonomy and duration claims (publisher
  pages returned HTTP 403 throughout this session).
- Peer-reviewed publication status of Grober (2006) — currently only confirmed as an arXiv preprint.
- Exact publication year/venue of the Cheetham X-Factor Stretch paper (2001 vs 2008 conflict).
- Exact year of Brown/Selbie/Wallace X-factor-methodology paper.
- Primary-source confirmation of Hellström (2009).
- Exact absolute X-factor degree values by group from Meister et al. (2011) — only correlation
  coefficients were confirmed.
- Millisecond timing offsets between pelvis/thorax/arm/club peak angular velocities — only relative
  ordering, not gaps, is sourced.
- Percentage of amateurs achieving the "ideal" fully sequential kinematic pattern.
- Iron-specific (and 8-iron-specific) phase-duration data — none found; all duration data is driver-
  based or club-unspecified.
- Provenance/creator/date of the P1–P10 coaching system.
- Whether a gait-style decile/percentile time-normalisation protocol exists anywhere in golf-EMG
  literature.
- Primary-source confirmation of the "0% / 100% (impact) / 140% (follow-through end)" normalisation
  claim.
