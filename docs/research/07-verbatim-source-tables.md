# Verbatim source tables — McHardy & Pollard 2005, Kim et al. 2004, Pink et al. 1990

Direct extractions from publisher-typeset full text, not summaries. These are the closest thing to primary
numeric data obtained in this project, and they fill the scapular gap flagged in
`02-trunk-and-core-activation.md`.

Provenance note: this extraction was relayed by a peer research session. The Kim et al. 2004 citation was
**independently verified against PubMed** by this session before acceptance — Kim DH, Millett PJ, Warner JJP,
Jobe FW. "Shoulder injuries in golf." Am J Sports Med. 2004;32(5):1324-30. **PMID 15262661.** Confirmed real.

## READ FIRST — the single most dangerous misreading in this project

**McHardy & Pollard Table 3 and Table 4 list only the two most-active muscles per side per phase.**

They are **not** activation grids. A muscle absent from a cell means "not in the top two for that side and
phase" — it does **not** mean inactive, and it does **not** mean no data.

Muscles with no value anywhere in that paper despite being active: lower trapezius, rhomboids in four of five
phases, levator scapulae in four of five phases, and latissimus dorsi in **all** five phases.

**For an app animating continuous activation, blank cells must never be read as zero.** Kao et al. 1995
measured all four scapular groups bilaterally across all five phases; McHardy reproduces only the fraction
that made the top two.

## McHardy & Pollard 2005 — Table 3, verbatim

Br J Sports Med 2005;39:799-804, doi:10.1136/bjsm.2005.020271, PMC1725059.

Caption as printed: "Summary of most active muscles in upper body/trunk during the different phases of the
golf swing (percentage of maximal manual testing)". Left = lead, right = trail (right-handed golfer).

| Phase | Left (lead) | Right (trail) |
|---|---|---|
| Back swing | Subscapularis 33%; Upper serratus 30% | Upper trapezius 52%; Middle trapezius 37% |
| Forward swing | Rhomboid 68%; Middle trapezius 51% | Pectoralis major 64%; Upper serratus 58% |
| Acceleration | **Pectoralis major 93%**; Levator scapulae 62% | **Pectoralis major 93%**; Upper serratus 69% |
| Early follow through | Pectoralis major 74%; Infraspinatus 61% | Pectoralis major 74%; Subscapularis 64% |
| Late follow through | Infraspinatus 40%; Pectoralis major 39% | Subscapularis 56%; Upper and lower serratus 40% |

Units are **%MMT** — peak one-second EMG during manual muscle strength testing = 100%. Not dynamometer %MVC.
Table 3 carries **no footnote**; the caption is the only unit definition.

Source typography preserved: the paper prints "Middle trapezuis (37%)" (misspelled) in one cell and
"Middle trapezius (51%)" in another; "pectoralis major (39%)" with a lowercase initial. Infraspinatus carries
values in Table 3 but is **missing from Table 2's muscle inventory** — an error in the source, flagged not
corrected.

## McHardy & Pollard 2005 — Table 4, verbatim (lower body)

| Phase | Left (lead) | Right (trail) |
|---|---|---|
| Back swing | Erector spinae 26%; Abdominal oblique 24% | Semimembranosus 28%; Long head biceps femoris 27% |
| Forward swing | **Vastus lateralis 88%**; Adductor magnus 63% | **Upper and lower gluteus maximus 100% and 98%**; Biceps femoris 78% |
| Acceleration | Biceps femoris 83%; Upper and lower gluteus maximus, vastus lateralis 58% | Abdominal oblique 59%; Gluteus medius 51% |
| Early follow through | Long head biceps femoris 79%; Vastus lateralis 59% | Gluteus medius 59%; Abdominal oblique 51% |
| Late follow through | Semimembranosus and vastus lateralis 42%; Adductor magnus 35% | Vastus lateralis 40%; Gluteus medius 22% |

Body text renders one value as "(100% MMT and 98% MM)" — "MM" is a source typo for "MMT".

**This forces a revision to F-012.** Trail gluteus maximus here reaches 100% and 98% %MMT in forward swing,
against the 62–72% **%EMGmax** recorded from Marta et al. 2013. These are different units (F-010) and are not
directly comparable — but both identify trail gluteus maximus as the dominant muscle of the downswing, from
independent studies and independent normalisation methods. That convergence is itself the strongest signal in
the dataset.

## Kim et al. 2004 — Table 2, the complete scapular grid

Am J Sports Med 2004;32(5):1324-1330, PMID 15262661. Caption: "Relative EMG Activity of Scapular Stabilizer
Muscles During the Golf Swing for a Right-Handed Golfer". Footnote: "+, approximately 15%-20% of maximal
manual muscle testing."

This is **qualitative ordinal** data (+ to +++++), not numeric percentages, and it is a **secondary
reproduction** — Kim explicitly attributes it to Kao et al. 1995 (their ref 21). It is nonetheless the only
complete four-muscle, both-sides, all-phases scapular grid located anywhere.

Kim's phase scheme differs from McHardy's: Kim splits takeaway from backswing and does **not** split
follow-through. **Do not merge the two grids cell-to-cell without accounting for this.**

| Muscle | Side | Takeaway | Backswing | Downswing | Acceleration | Follow-through |
|---|---|---|---|---|---|---|
| Levator scapulae | Trail (R) | + | + | ++ | ++ | + |
| Levator scapulae | Lead (L) | — | — | ++ | +++ | ++ |
| Rhomboids | Trail (R) | + | + | ++ | ++ | + |
| Rhomboids | Lead (L) | — | — | +++ | +++ | ++ |
| Trapezius | Trail (R) | ++ | ++ | + | + | + |
| Trapezius | Lead (L) | — | — | ++ | ++ | + |
| Serratus anterior | Trail (R) | — | — | ++ | +++ | ++ |
| Serratus anterior | Lead (L) | + | + | + | + | + |

**Alignment caveat, flagged by the extractor:** the left-side rows print fewer "+" marks than there are
columns. Alignment to the right-hand columns was inferred from the paper's own narrative, which corroborates
every row. The pattern is reliable; the exact blank/non-blank boundary is inference, not print.

Corroborating narrative, Kim p.1325 verbatim:

> "The trapezius muscle helped to retract the scapula and showed the greatest activity during the downswing
> and acceleration phases for the lead arm, whereas peak activity of the trapezius in the trailing arm
> occurred during takeaway. For the rhomboid and levator scapulae muscles of the lead arm, scapular
> retraction and elevation were most active during the downswing and acceleration phases—for the trailing
> arm, both muscles were also active during the downswing to help with scapular protraction and overall
> scapular stabilization. Finally, the serratus anterior muscle acted mainly as a scapular protractor and
> demonstrated peak activity during the downswing, acceleration, and follow-through phases of the trailing
> arm. In contrast, for the leading arm, the serratus anterior exhibited low, synchronized activity
> throughout the entire swing, which may explain why it can be susceptible to fatigue in some golfers."

That last clause is directly useful: constant low lead-side serratus activity across the whole swing is a
distinctive pattern worth showing, and it explains a real fatigue mechanism in golfers.

## Pink, Jobe & Perry 1990 — the full shoulder grid (%MMT, n=13 professionals)

The primary paper is paywalled, but this grid **cross-checks 20 of 20 values against McHardy & Pollard's
independently verified Table 3**. That is a strong validation: every value that appears in both sources
agrees exactly. High confidence.

**Trail (right) side**

| Muscle | Back swing | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 12 | 64 | **93** | 74 | 37 |
| Subscapularis | 16 | 49 | **68** | 64 | 56 |
| Supraspinatus | **25** | 14 | 12 | 7 | 7 |
| Infraspinatus | **27** | 13 | 7 | 12 | 9 |
| Anterior deltoid | 5 | **21** | 10 | 11 | 8 |

**Lead (left) side**

| Muscle | Back swing | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 21 | 18 | **93** | 74 | 39 |
| Subscapularis | **33** | 29 | 41 | 23 | 35 |
| Supraspinatus | 21 | 21 | 18 | **28** | 28 |
| Infraspinatus | 14 | 16 | 27 | **61** | 40 |
| Anterior deltoid | 13 | 9 | 10 | 21 | **26** |

**Middle and posterior deltoid** span 2–8% and 5–24% respectively across all phases with **no discernible
pattern** — quantitatively non-contributory. Jobe, Moynes & Antonelli 1986 state this directly: deltoid was
inactive on the trail side throughout, and "likewise inactive on the left [lead] except for a brief spurt
from the anterior portion during the milliseconds immediately preceding ball contact."

This is a genuine finding worth rendering, not a gap: two large, visually prominent shoulder muscles do
almost nothing in the golf swing. Exactly the contrast the user asked to preserve.

### The identical 93/93 is real, and it is the most interesting number in the dataset

Pectoralis major reads **93% on both sides simultaneously** at acceleration, and 74% on both sides at early
follow-through. Confirmed against the primary McHardy PDF — not a transcription error.

McHardy's own discussion explains the mechanism: the **trail** pectoralis contracts **concentrically**,
driving internal rotation and adduction. The **lead** pectoralis contracts **eccentrically** at comparable
amplitude, braking and controlling arm abduction and external rotation.

**Identical EMG amplitude, opposite mechanical role.** This is a fundamental limitation of what colour alone
can express: our visualisation will show both sides equally red at impact while they are doing opposite
jobs. Worth considering whether the app should distinguish concentric from eccentric work.

### The dominant organising pattern of the whole upper body

**Trail side peaks early; lead side peaks late.** This holds for supraspinatus, infraspinatus, middle
trapezius, anterior deltoid and the wrist extensors alike. Infraspinatus is the clearest case: trail peaks at
back swing (27%) then falls to 7–12%, while lead climbs to 61% at early follow-through.

The trail side positions and drives; the lead side stabilises then decelerates. Subscapularis and pectoralis
major are the exceptions, peaking together at acceleration.

**Corroborated by injury epidemiology:** over 90% of golfers' shoulder injuries involve the **lead** shoulder,
roughly three times the trail rate (Kim et al. 2004) — consistent with the lead cuff absorbing deceleration
load.

### Confidence differs sharply by body region

The shoulder and scapular data is **single-lab, single-era, never replicated** — Kerlan-Jobe, 1986–1995,
n=7–15 per study. The forearm has **five independent modern replications** (Farber 2009, Sorbie 2016/2017,
Robinson 2023, Bochnia 2024, Grieß 2026). Weight confidence accordingly: forearm findings are robust,
shoulder findings rest on one laboratory's work from three decades ago.

## Latissimus dorsi — numbers at last, and a three-way dispute

`02-trunk-and-core-activation.md` recorded that no numeric latissimus value existed in any accessible source.
That gap is now partially closed.

**Pink et al. 1990, per-phase %MMT:**

| Side | Takeaway | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Trail (R) | 9 | **50** | 47 | 39 | 28 |
| Lead (L) | 17 | **46** | 31 | 32 | 18 |

Peak is forward swing bilaterally. **Single-source caveat:** these came from an OCR extraction that could not
be cross-validated for latissimus specifically, because latissimus never appears in McHardy Table 3 so no
independent check was possible. Nine other muscle values from the same extraction cross-validated 9/9 against
McHardy Table 3, so the extraction is demonstrably faithful overall — but treat the latissimus row as
single-source.

**Kim et al. 2004 Table 1, qualitative:** Trail — downswing +++, acceleration +++, follow-through ++, blank
takeaway/backswing. Lead — takeaway +, backswing +, downswing +++, acceleration ++, follow-through +.

**The dispute on peak phase — report the range, do not pick a winner:**

- Pink et al. 1990: **forward swing**
- Kim et al. 2004: **downswing and acceleration**
- Marta et al. 2012: **acceleration** ("The pectoralis major, subscapularis and latissimus dorsi muscles of
  both sides showed their peak activity during the acceleration phase.")

Likely a phase-boundary artefact — Pink's "forward swing" is the early downswing, which is Kim's "downswing"
column — but the sources genuinely differ as printed.

Kim p.1325 verbatim on the two dominant shoulder muscles:

> "The latissimus dorsi and the pectoralis major demonstrated the most activity of all the shoulder muscles,
> with the latissimus dorsi acting maximally during the downswing and acceleration phases, whereas the
> pectoralis major demonstrated activity later in the swing, during acceleration and follow-through."

## Forearm — what McHardy actually says

McHardy contains **no numeric value for any forearm or wrist muscle**, and forearm muscles are not even
listed in its Table 2 inventory. Do not cite it for any forearm number. What it does say, verbatim:

> "In the forearms, there is what is termed the ''flexor burst'' during this phase. This refers to a large
> increase in wrist flexor muscle activation just before the point of impact."

> "Just before impact there is an increase in right wrist flexor activation, the flexor burst, which
> corresponds to combined flexion and pronation of the right forearm that occurs through impact. If there is
> a sudden decrease in clubhead acceleration—for example hitting the ground or tree root etc—there is a
> sudden change from concentric to eccentric contraction in the wrist flexors."

The flexor burst is attributed to the **trail (right)** side. No statement is made about lead-side wrist
flexors.

## Swing phase definitions, verbatim

McHardy & Pollard pp.799-800:

> "Back swing: ball address to top of back swing / Forward swing: top of swing to club horizontal (early part
> of down swing) / Acceleration: horizontal club to impact (late part of down swing) / Early follow through:
> impact to horizontal club / Late follow through: horizontal to completion of swing"

**This contradicts F-008 and must be reconciled.** McHardy explicitly defines acceleration as ending **at**
impact (pre-impact), while the Bechler/Marta lineage places it after impact. So the two conventions exist
*within* the peer-reviewed literature itself, not merely between research and coaching. F-008's remedy still
holds and becomes more important: never rely on the phase label, always check the source's own definition.

Note also that Figure 1 labels **eight** photographic positions (address, early back swing, late back swing,
top of swing, down swing, acceleration, early follow through, late follow through) while the text defines
five phases. The figure is not a phase scheme.

Minor internal inconsistency preserved: the bullet list starts back swing at "ball address", the body text at
"the time the club starts movement".

## Methodological warnings

**No banding scheme exists in McHardy.** No low/moderate/high thresholds of any kind — raw %MMT only. The
ordinal + to +++++ scheme belongs to Kim, not McHardy. Do not attribute a banding scheme to McHardy.

**Electrode types are pooled silently.** The paper states "Either the Basmajian single needle technique or
surface electrodes were used" across the pooled studies, then tabulates all resulting %MMT values together
without distinguishing which came from which. Indwelling fine-wire and surface EMG are not interchangeable —
surface electrodes cannot validly record supraspinatus or subscapularis at all, and crosstalk differs
markedly. **Treat cross-muscle magnitude comparisons within Table 3 as provisional.**

**Skill-level caveat, McHardy p.803 verbatim:**

> "most studies were conducted on highly skilled golfers (professional or low handicap, <5, amateurs). In the
> United States, the average handicap is 16.1 for male golfers and 29.2 for female golfers... Although the
> data collected may represent what ideally should occur during the golf swing, it may not accurately reflect
> the actual swings of most golfers. The ''average'' golfer is a very different quality of player, who would
> be expected to have a less reproducible and efficient golf swing, with potentially different muscle
> activity during the swing from a highly skilled golfer. Extrapolation of the data from one cohort to the
> other may therefore be problematic."

**Handedness caveat, p.803 verbatim — directly relevant to D-007:**

> "All of the golfers selected in the studies were right handed. This aids standardisation of the data...
> However, left and right handed golfers may be different, and it is an assumption that EMG activity in the
> left handed golfer is a mirror image of the right handed golfer."

The left-handed mirror in D-007 is therefore an assumption the literature itself flags as unverified, not an
established equivalence. It remains the right implementation choice, but should be labelled.

**Swing-type caveat:** the source studies never describe which swing type subjects used (classic, modern, or
hybrid), each of which has distinct body motion that may alter activation.

## Sources

- McHardy A, Pollard H. Muscle activity during the golf swing. Br J Sports Med. 2005;39(11):799-804.
  PMC1725059. https://pmc.ncbi.nlm.nih.gov/articles/PMC1725059/
- Kim DH, Millett PJ, Warner JJP, Jobe FW. Shoulder injuries in golf. Am J Sports Med. 2004;32(5):1324-1330.
  PMID 15262661. https://journals.sagepub.com/doi/10.1177/0363546504267346
- Kao JT, Pink M, Jobe FW, Perry J. Electromyographic analysis of the scapular muscles during a golf swing.
  Am J Sports Med. 1995;23(1):19-23. PMID 7726345. (Primary source of the Kim Table 2 data; not directly accessed.)
- Pink M, Jobe FW, Perry J. Electromyographic analysis of the shoulder during the golf swing.
  Am J Sports Med. 1990;18(2):137-140. PMID 2343980.
- Marta S, et al. Electromyography variables during the golf swing: a literature review.
  J Electromyogr Kinesiol. 2012;22(6):803-813. PMID 22542769.
- Glazebrook MA, Curwin S, Islam MN, et al. Medial epicondylitis. An electromyographic analysis and an
  investigation of intervention strategies. Am J Sports Med. 1994;22:674-679.
