# Trunk and core activation by swing phase

Lead = left side, trail = right side, right-handed golfer, throughout.

## Normalisation warning — these units are not interchangeable

Three incompatible normalisation methods appear across the trunk literature:

- **%MMT** — manual muscle test reference (Pink / Jobe / Perry / Watkins series)
- **%MVC** — isometric maximum reference (Sorbie, Li, Cole & Grimshaw)
- **%EMGmax** — peak within the swing itself (Marta et al.)

A muscle at "60%" in one study is not comparable to "60%" in another. Every figure below is labelled.
This is the single largest obstacle to building one unified activation model and must be handled explicitly
in T-012.

Also: the literature resolves **5 phases**, not 9. Address, top of backswing and impact are treated as
boundary *instants*, never as sampled bins — no study measures them. Any value the app shows at address or
impact is interpolation, not measurement.

## Erector spinae — best instrumented, and genuinely disputed

### Li et al. 2023 (n=8 recreational golfers, 18.8±1.2 hcp, T8 thoracic and L3 lumbar, %MVC)

This is the highest-resolution dataset located — full five-phase, bilateral, both spinal regions.

| Phase | Lead T8 | Trail T8 | Lead L3 | Trail L3 |
|---|---|---|---|---|
| Backswing | 13.7±2.5 | 21.6±3.9 | 17.1±4.3 | 12.6±2.9 |
| Forward swing | 21.6±2.8 | 24.7±3.7 | 24.4±4.1 | 22.1±3.2 |
| Acceleration | 39.2±4.9 | 34.0±3.4 | **48.8±4.1** | 46.9±3.4 |
| Early follow-through | **51.8±3.9** | 28.0±3.8 | 39.3±4.0 | 38.1±4.9 |
| Late follow-through | 30.9±3.8 | 19.5±4.3 | 22.4±3.2 | 26.8±4.5 |

### Sorbie et al. 2018 (n=15 right-handed males, four clubs, T8/L1/L5, sides pooled, %MVC)

| Phase | %MVC |
|---|---|
| Forward swing | 67–99 |
| Acceleration | 83–106 |

No significant lead/trail or club difference found. Values above 100% are the dynamic-versus-static-MVC
artefact documented in `06-activation-curve-and-colour-method.md`, not literal supramaximal contraction.

### The dispute

**Sorbie (67–106% MVC) and Li (13–52% MVC) diverge by two to three times for the same muscle group.**
Plausible causes: different electrode sites (L1/L5 versus L3), different skill and age mixes, different MVC
reference contractions. **Not reconciled — the app must carry both ranges rather than picking one.**

### Two further erector spinae findings

**The lead thoracic peak arrives a phase later than expected.** Li's data shows lead T8 peaking at
**early follow-through (51.8%)**, not acceleration — contradicting the older MMT-based narrative that
everything peaks at acceleration. Plausibly a real thoracic-versus-lumbar regional difference that
single-electrode-site studies could not detect. Flagged, unresolved.

**Low back pain reverses direction by skill tier** (Cole & Grimshaw 2008): low-handicap golfers with LBP
show *reduced* erector spinae at top of backswing and impact versus low-handicap controls, paired with
*increased* external oblique. High-handicap golfers with LBP show the *opposite* — increased erector spinae.
Not a monotonic effect. LBP golfers also activate erector spinae **earlier**, before backswing initiation —
a timing effect, not an amplitude one.

Pink et al. 1993: erector spinae (pooled with oblique signal) <30% MMT at takeaway, >30% MMT for the rest of
the swing, except lead side dropping to 28% MMT at late follow-through.

## Gluteus maximus — the highest verified value in the entire review

| Phase | Lead | Trail |
|---|---|---|
| Forward swing / acceleration | elevated, not quantified | **62–72% EMGmax** |

Marta et al. 2013 (n=9). **This is the single highest verified activation value found across every muscle in
every strand of this research**, narrowly ahead of trail external oblique. Consistent with its role anchoring
pelvic rotation, against which the trunk generates X-factor stretch.

Do not merge with Ghigiarelli et al. 2014's figures (lead 17.4–31.6%, trail 36.4–53.4% MVIC) — those are
from a training drill, not a swing.

Claims circulating in non-peer-reviewed coaching content ("glutes fire near 100% voluntary effort", "35%
amplitude reduction as a swing-fault marker") are **excluded** — no peer-reviewed source.

## External oblique

| Phase | Lead | Trail |
|---|---|---|
| Takeaway/backswing | <30% MMT | <30% MMT; elevated in low-handicap LBP golfers at top |
| Early downswing | high | high |
| Late downswing / acceleration | high | **59–67% EMGmax** |
| Early follow-through | mod–high; +3% MVC with 4-iron vs pitching wedge (p=.032) | mod–high |
| Late follow-through | >30% MMT | 28% MMT |

**Open discrepancy:** the Marta/Silva 2012 systematic review characterises obliques as "moderate to low"
overall, while Marta's own 2013 primary data gives trail EO at 59–67% EMGmax — a very-high band. Most likely
a %MMT-versus-%EMGmax normalisation artefact rather than a physiological contradiction, but reported as
unresolved.

## Rectus abdominis

No study yields a full numeric table. Watkins et al. 1996 measured upper and lower RA bilaterally across all
five phases, but the full text is paywalled and the figures are unverified. Directionally: <30% MMT during
takeaway/backswing, moderate through downswing, sub-peak relative to external oblique.

Quinn et al. 2022 (n=33 elite golfers, 17 developed LBP over 6 months): trail-side RA activation elevated at
multiple time-points in those who went on to develop low back pain — a relative group difference, no absolute
values.

Structural correlate (MRI, not EMG): skilled golfers show dominant-side RA hypertrophy, +6.36±6.50% volume
asymmetry versus −2.12±9.64% in non-golfers (Izumoto et al. 2019).

## Latissimus dorsi

| Phase | Lead | Trail |
|---|---|---|
| Takeaway/backswing | low | low |
| Early downswing | moderate, rising | **"marked activity" — described as the primary power contributor of this phase** |
| Late downswing / acceleration | moderate–high | high (peak) |
| Early follow-through | moderate | elevated |

**No numeric %MVC value for latissimus dorsi exists at any phase in any accessible source.** Pink, Jobe &
Perry 1990 — the primary source measuring eight shoulder muscles bilaterally — is available only as an
abstract giving qualitative timing. Quinn et al. 2022 found trail-side lat activation elevated at multiple
time-points in golfers who later developed LBP.

## Serratus anterior

Kao et al. 1995 (n=15 competitive male golfers) is the only study specifically targeting serratus anterior in
golf. Findings are qualitative: activity is **constant** in the lead arm across the whole swing, and **high in
the trail arm from forward swing onward** to maximise scapular protraction. The constant lead-side pattern is
noted as a fatigue-risk marker in high-volume golfers.

One numeric anchor exists — **58% MMT**, trail side, second-most-active muscle in McHardy & Pollard's
nine-study, seventeen-muscle synthesis (behind pectoralis major at 64% MMT). **Phase attribution is inferred,
not stated**, and the primary source within the review could not be traced. Low confidence.

## Muscles with no golf EMG data at all

Three independent research passes converged on the same three hard gaps, which increases confidence that
these are real features of the literature rather than search failures:

- **Transversus abdominis** — no fine-wire (or any) EMG study during an actual golf swing exists. Surface EMG
  cannot isolate it from overlying internal oblique. One tangential study uses ultrasound thickness as an
  indirect proxy, not EMG; full text inaccessible.
- **Multifidus** — no golf-specific EMG data, surface or fine-wire. Cole & Grimshaw comment interpretively
  that LBP golfers appear to rely on erector spinae "rather than deeper spinal muscles like transversus
  abdominis and multifidus" — an inference, not a measurement.
- **Quadratus lumborum** — no direct EMG measurement in golf. One paper estimates QL force via an
  EMG-assisted optimisation model using *other* muscles as input; PDF unreadable, unverified. Non-golf
  fine-wire work shows QL up to ~74% MVC under heavy axial loads — background only, not golf evidence.

**Internal oblique** is a near-gap: Horton et al. 2001 measured it bilaterally in elite golfers but reports no
amplitude values, only that RMS did not differ between chronic-LBP and asymptomatic groups. The single
recoverable number is a lead-side +1% MVC difference between 4-iron and pitching wedge — statistically
significant, magnitude trivial.

## Peak activation summary

| Muscle / side | Peak phase | Magnitude | Confidence |
|---|---|---|---|
| Gluteus maximus, trail | Forward swing → acceleration | 62–72% EMGmax | Moderate — single study |
| External oblique, trail | Late downswing / acceleration | 59–67% EMGmax | Moderate — single study, corroborated directionally |
| Erector spinae | Acceleration (classic); lead thoracic peaks at early follow-through per Li | 13–52% (Li) vs 67–106% (Sorbie) | **Disputed — carry both** |
| Latissimus dorsi, trail | Acceleration | Qualitative only | Low — no numeric value exists |
| Rectus abdominis | Acceleration | Moderate, sub-peak vs EO | Low — no numeric table |
| Serratus anterior, trail | Forward swing → acceleration (inferred) | 58% MMT | Low — phase inferred |
| Internal oblique | Undetermined | Undetermined | Very low |
| Transversus abdominis, multifidus, quadratus lumborum | — | — | **None — no data exists** |

## X-factor and the trunk

X-factor is shoulder-pelvis rotational separation at top of backswing; X-factor *stretch* is the further
increase during transition as the pelvis begins forward rotation while the shoulders still lag — a
stretch-shortening-cycle mechanism.

Cheetham's work (accessed via secondary synthesis only, primary paper not located) reports that X-factor
magnitude at top of backswing **does not significantly differ** between highly-skilled and less-skilled
golfers — it is X-factor *stretch* that differentiates skill. Reported stretch magnitude is inconsistent
across secondary sources: "15–19%" versus "as much as 15°", an unresolved unit discrepancy. Skilled
(sub-10-handicap) golfers reach ~70° peak separation.

Cole & Grimshaw's review describes the modern swing as restricting pelvic rotation while increasing thoracic
rotation during backswing, preloading trunk muscles to store elastic energy — and links the same pattern to
elevated lumbar spine forces and LBP risk.

An 8-week core-stability intervention produced both a significant oblique activation increase and a
significant X-factor increase (Arch Phys Med Rehabil 2024, authors unconfirmed) — suggestive of a trainable
link, single study, effect sizes unrecoverable.

**Critically: no study directly correlates trunk EMG amplitude with X-factor degrees or resulting clubhead
speed.** This causal link is routinely assumed in coaching literature and is **not substantiated by any
verifiable primary EMG source**. The attribution of X-factor stretch to the obliques and erector spinae is
secondary synthesis, not paired EMG-kinematic measurement.

## Skill differences

**No study directly compares trunk %MVC between skill tiers with matched methodology.** The landmark studies
(Pink 1993, Watkins 1996) sampled elite golfers only, with no amateur comparison arm. A circulating figure of
~90% MVC for amateurs versus ~80% for professionals with a 5-iron has untraceable internal attribution and
should be used cautiously if at all.

What is established: amateurs show less lead-side lateral bend in forward swing, associated with greater
trail-side erector spinae activation than skilled golfers (Bulbulian et al.). Among elite golfers with
chronic LBP, amplitude did not differ from asymptomatic peers — only activation **onset timing** was delayed
(Horton et al. 2001). Magnitude and timing are dissociable.

## Verification status

| Item | Status |
|---|---|
| Transversus abdominis, multifidus, quadratus lumborum | **No data exists** — confirmed by three independent passes |
| Internal oblique amplitude by phase | Not found — measured but unreported |
| Watkins 1996 exact %MMT figures | Paywalled, unverified |
| Pink 1993 full phase table | Paywalled beyond the <30% / >30% / 28% thresholds |
| Serratus anterior 58% MMT | Single source, phase inferred, primary attribution untraceable |
| Latissimus dorsi numeric %MVC | Does not exist in any accessible source |
| Erector spinae magnitude | **Genuinely disputed** (Li vs Sorbie) — not reconciled |
| Address phase, all muscles | Never measured as a bin — assumed near-resting |
| Professional vs amateur trunk EMG | No matched-methodology comparison found |
| Cheetham X-factor-stretch magnitude | Inconsistent across secondary sources; primary not located |
| Direct EMG-to-X-factor correlation | **Not found** — assumed in coaching literature, never demonstrated |

## Key references

1. Pink M, Perry J, Jobe FW. Electromyographic analysis of the trunk in golfers. Am J Sports Med. 1993;21(3):385–388. PMID 8346752.
2. Pink M, Jobe FW, Perry J. Electromyographic analysis of the shoulder during the golf swing. Am J Sports Med. 1990;18(2):137–140. PMID 2343980.
3. Watkins RG, Uppal GS, Perry J, Pink M, Dinsay JM. Dynamic EMG analysis of trunk musculature in professional golfers. Am J Sports Med. 1996;24(4):535–538. PMID 8827315.
4. Kao JT, Pink M, Jobe FW, Perry J. EMG analysis of the scapular muscles during a golf swing. Am J Sports Med. 1995;23(1):19–23. PMID 7726345.
5. Marta S, Silva L, Vaz J, Bruno P, Pezarat-Correia P. EMG analysis of trunk muscles during the golf swing performed with two different clubs. Int J Sports Sci Coach. 2013;8(4):779–788.
6. Marta S, et al. Electromyography variables during the golf swing: a literature review. J Electromyogr Kinesiol. 2012;22(6):803–813. PMID 22542769.
8. Cole MH, Grimshaw PN. EMG of the trunk and abdominal muscles in golfers with and without low back pain. J Sci Med Sport. 2008;11(2):174–181. PMID 17433775.
12. Sorbie GG, Grace FM, Gu Y, Baker JS, Ugbolue UC. EMG analyses of the erector spinae muscles during golf swings using four different clubs. J Sports Sci. 2018;36(7):717–723. PMID 28594287.
13. Li B, et al. Effects of Ground Slopes on Erector Spinae Muscle Activities and Characteristics of Golf Swing. Int J Environ Res Public Health. 2023;20(2):1176.
14. McHardy A, Pollard H. Muscle activity during the golf swing. Br J Sports Med. 2005;39(11):799–804.
15. Horton JF, Lindsay DM, Macintosh BR. Abdominal muscle activation of elite male golfers with chronic low back pain. Med Sci Sports Exerc. 2001;33(10):1647–1654.
17. Quinn SL, Olivier B, McKinon W, Dafkin C. Increased trunk muscle recruitment during the golf swing is linked to developing lower back pain. J Electromyogr Kinesiol. 2022;64:102663. PMID 35526433.
18. Izumoto Y, Kurihara T, Suga T, Isaka T. Bilateral differences in the trunk muscle volume of skilled golfers. PLoS ONE. 2019;14(4):e0214752. (MRI, not EMG.)
