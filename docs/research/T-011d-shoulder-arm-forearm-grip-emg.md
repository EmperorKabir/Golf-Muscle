# T-011d — Shoulder Girdle, Arm, Forearm and Grip EMG During the Golf Swing

Scope: upper-limb muscle activation (shoulder girdle → hand/grip) by swing phase, lead (left, for a
right-handed golfer) vs trail (right) side. Companion to [[T-011a-phase-taxonomy-and-timing]] for the
swing-phase model, and to the trunk/lower-limb strands (T-011b/c) for the rest of the kinetic chain.

**Session constraint, same as the phase-taxonomy pass:** the project's WebSearch budget (200 calls) was
already exhausted by concurrent research passes before this pass could run any. All research below was
done via `WebFetch` against PubMed, PubMed Central, Europe PMC, Semantic Scholar/Crossref metadata
endpoints, DuckDuckGo's HTML interface (used only as a fetch target, not the WebSearch tool), and direct
publisher/repository/PDF URLs. This reaches most of the same material but is slower and hits more
paywalls/CAPTCHAs than free-form search would. Gaps caused by this are flagged inline, not silently
filled. Piracy mirrors (sci-hub and similar) turned up in search results and were **not used** — every
number below traces to a legitimate publisher, PubMed/PMC/Europe PMC record, or an author/conference
open copy.

---

## 0. Critical methodology warning — do not merge these numbers naively

Four incompatible measurement conventions appear below. Treating them as one continuous scale will
silently corrupt the activation model:

| Convention | Used by | Notes |
|---|---|---|
| **% MVC** (maximum voluntary contraction) | Glazebrook et al. 1994 | True normalised EMG; values should not exceed ~100% except brief bursts. |
| **% of maximal manual muscle test (MMT)** | Farber et al. 2009 | Kerlan-Jobe lineage's own reference contraction, clinician-resisted, submaximal by design. Values routinely **exceed 100%** (e.g. 120.9% reported) because the golf-swing contraction can surpass the resisted-test reference. **Not numerically comparable to true %MVC without a conversion factor that no source supplies.** |
| **% MVIC** (maximum voluntary isometric contraction) | Escamilla & Andrews 2009 (review) | Functionally the same concept as %MVC; different label, same normalisation logic. |
| **Raw surface EMG amplitude (µV)** | Bochnia et al. 2024; Grieß et al. 2026 | Not normalised at all — depends on electrode placement, skin impedance, subject-specific tissue properties. Only within-study, within-subject relative comparisons (phase-to-phase, lead-vs-trail, condition-vs-condition) are valid; absolute µV numbers must never be read as %MVC or compared across studies. |

The classic Kerlan-Jobe/Centinela shoulder and scapular papers (Jobe 1986, Jobe 1989, Pink 1990, Kao
1995) are described in their own abstracts and in secondary reviews largely in **qualitative** terms
(“active during acceleration”, “relatively noncontributory”) — the quantitative %MVC tables in those
papers exist in the original print journal but were not extractable through any accessible legitimate
route this session (SAGE/AJSM paywall; see §9 gaps). Where a number is genuinely absent, this document
says so rather than inventing one.

---

## 1. Swing-phase model used below

Per [[T-011a-phase-taxonomy-and-timing]], the EMG literature standard is the **5-phase Jobe/Pink/Perry/Kao
scheme**, confirmed again independently in this pass via Grieß et al. 2026, which states verbatim that it
uses “the five phases of the golf swing according to Jobe et al.”:

1. **Takeaway** — address → top of backswing (spans the entire backswing; no separate “address” or
   “late backswing” checkpoint in this scheme).
2. **Forward swing** — top of backswing → club shaft horizontal in the downswing.
3. **Acceleration** — club horizontal (downswing) → ball contact/impact.
4. **Early follow-through** — impact → club horizontal in follow-through.
5. **Late follow-through** — club horizontal (follow-through) → finish.

**Glazebrook et al. 1994 (wrist/forearm) uses a different, four-phase scheme that explicitly includes a
static Address timepoint** (“ranging from 33.59% MVC at address to 58.77% at contact” — implying Address
is phase 1 of their own 4-phase division, distinct from the Jobe 5-phase scheme). The exact names of
Glazebrook's other three phases were not recoverable from the accessible abstract — flagged as a gap.

**Mapping onto the brief's requested 9-phase scheme** (address / takeaway–early backswing / late
backswing / top–transition / early downswing / late downswing–acceleration / impact / early
follow-through / late follow-through) is therefore approximate for anything sourced from the 5-phase
literature:

| Brief's 9-phase scheme | Nearest Jobe 5-phase equivalent |
|---|---|
| Address | Not a distinct phase in the 5-phase scheme (start-point of Takeaway); only Glazebrook reports address as its own data point |
| Takeaway / early backswing | Early portion of **Takeaway** |
| Late backswing | Late portion of **Takeaway** |
| Top / transition | End-point of **Takeaway** / start-point of **Forward swing** |
| Early downswing | **Forward swing** |
| Late downswing / acceleration | **Acceleration** |
| Impact | End-point of **Acceleration** / start-point of **Early follow-through** |
| Early follow-through | **Early follow-through** |
| Late follow-through | **Late follow-through** |

All tables below use the **source studies' own phase names** (Takeaway / Forward swing / Acceleration /
Early follow-through / Late follow-through, or Glazebrook's own wording) rather than force-fitting numbers
into the 9-phase brief, to avoid misattributing a value to a phase boundary the original authors did not
measure. Use the mapping table above to place them on the app's timeline.

---

## 1A. Recovered numeric tables — Pink 1990 and McHardy & Pollard Table 3

Added on a second research pass. An earlier pass recorded "no numeric %MVC value recoverable" for the
shoulder and scapular muscles; that is now **superseded** for the muscles below. Where §2 still says a
value could not be recovered, this section takes precedence.

Two routes produced numbers where direct access to Pink 1990 and Kao 1995 failed:

- A scanned copy of **Pink M, Jobe FW, Perry J 1990** (13 professional golfers — 6 male, 7 female —
  indwelling fine-wire, 8 muscles bilaterally), giving a full 5-phase × 2-side grid.
- **McHardy A, Pollard H 2005** (*Br J Sports Med* 39(11):799–804, PMCID PMC1725059) **Table 3**, which
  lists the two most active muscles per side per phase with exact figures, drawn from Pink 1990 and
  Kao 1995. This is the **only** recovered numeric source for the scapular muscles.

Cross-validation: nine cells overlap between the two routes and agree exactly (9/9), which is why these
figures are reported rather than withheld. Non-peak cells rest on the scanned extraction alone and carry
lower certainty.

**Unit: %MMT (manual muscle test), not %MVC.** Do not place these on the same axis as Glazebrook's %MVC
figures or Escamilla's %MVIC ranges.

### Trail (right) shoulder — %MMT, Pink et al. 1990

| Muscle | Takeaway | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 12 | 64 | **93** | 74 | 37 |
| Subscapularis | 16 | 49 | **68** | 64 | 56 |
| Supraspinatus | **25** | 14 | 12 | 7 | 7 |
| Infraspinatus | **27** | 13 | 7 | 12 | 9 |
| Anterior deltoid | 5 | **21** | 10 | 11 | 8 |
| Middle deltoid | 2–8 across all phases, no pattern | | | | |
| Posterior deltoid | 5–24 across all phases, no pattern | | | | |

### Lead (left) shoulder — %MMT, Pink et al. 1990

| Muscle | Takeaway | Forward swing | Acceleration | Early FT | Late FT |
|---|---|---|---|---|---|
| Pectoralis major | 21 | 18 | **93** | 74 | 39 |
| Subscapularis | 33 | 29 | **41** | 23 | 35 |
| Supraspinatus | 21 | 21 | 18 | **28** | 28 |
| Infraspinatus | 14 | 16 | 27 | **61** | 40 |
| Anterior deltoid | 13 | 9 | 10 | 21 | **26** |
| Middle deltoid | 2–8 across all phases, no pattern | | | | |
| Posterior deltoid | 5–24 across all phases, no pattern | | | | |

Verbatim from Pink 1990 for the two low-activity heads: middle deltoid shows "low levels of activity for
all phases of the activity (2% to 8% MMT)"; posterior deltoid shows "low activity levels and no
significant differences nor pattern of activity throughout all phases for both the right and left sides
(5% to 24% MMT)".

**Flagged anomaly — now independently confirmed as printed.** Pectoralis major reads identically on both
sides at acceleration (93) and at early follow-through (74). [[07-verbatim-source-tables]] reproduces
McHardy's Table 3 directly and gives the same cross-side identities, so this **is** what the published
table prints — it is not an OCR error in this document's extraction. Whether McHardy's table faithfully
reflects Pink 1990's underlying per-side data, or itself collapsed two cells, cannot be checked without
the paywalled Pink original. Two identical cross-side values at two separate phases remains
physiologically surprising, so treat the *bilateral identity* claim (not the magnitude) as the uncertain
part.

### Scapular muscles — %MMT, McHardy & Pollard 2005 Table 3

**Critical reading rule — see [[07-verbatim-source-tables]].** Table 3 lists only the **two most active
muscles per side per phase**. It is *not* an activation grid. A blank means "not in the top two for that
side and phase" — it does **not** mean inactive and it does **not** mean no data. Kao 1995 measured all
four scapular groups bilaterally across all five phases; McHardy reproduces only the fraction that made
the top two. **For an animated app, blank cells must never be rendered as zero.**

| Phase | Lead (left) | Trail (right) |
|---|---|---|
| Back swing | upper serratus 30 | **upper trapezius 52**, middle trapezius 37 |
| Forward swing | **rhomboid 68**, middle trapezius 51 | upper serratus 58 |
| Acceleration | levator scapulae 62 | **upper serratus 69** |
| Early follow-through | — | — |
| Late follow-through | — | serratus anterior (upper + lower) 40 |

These %MMT figures are consistent in rank order with Escamilla & Andrews' pooled %MVIC ranges quoted in
§2.5–2.8 (trapezius 42–52%, rhomboids ~60%, levator scapulae ~60%, serratus anterior ~70%) — serratus
highest, trapezius lowest — despite the different normalisation. That agreement across two independent
normalisation methods raises confidence in the relative ordering, though not in the absolute values.

**Lower trapezius still has no recovered *numeric* value at any phase, on either side.** Kao 1995
instrumented upper, middle and lower trapezius separately, but only upper (52) and middle (37) surface in
Table 3.

**Qualitative fallback for the blank cells:** [[07-verbatim-source-tables]] reproduces **Kim et al. 2004
Table 2**, the only complete four-muscle, both-sides, all-phases scapular grid located anywhere. It is
**ordinal (+ to +++++), not numeric**, and is a secondary reproduction of Kao 1995, but it fills the shape
of the curves that Table 3 leaves blank — notably trail-side rhomboids and levator scapulae (both peaking
++ in downswing/acceleration) and the lead serratus anterior's flat low "+" across every phase. Kim's
phase scheme splits takeaway from backswing and does **not** split follow-through, so it cannot be merged
cell-to-cell with the table above.

---

## 2. Shoulder girdle muscles

### 2.1 Pectoralis major

- Sternal vs clavicular heads are **not distinguished in any located golf-swing EMG study** — every
  source treats pectoralis major as one muscle. Flagged as not found at sub-head resolution.
- **Jobe FW, Moynes DR, Antonelli DJ (1986)**, *Am J Sports Med* 14(5):388–392 (7 professional
  right-handed male golfers, indwelling EMG + 450 fps film): pectoralis major (with latissimus dorsi)
  “provided power during acceleration” phases. No %MVC figure recoverable from the accessible abstract.
- **Pink M, Jobe FW, Perry J (1990)**, *Am J Sports Med* 18(2):137–140 (8 shoulder muscles, both arms):
  “subscapularis and pectoralis major [active] during acceleration.”
- **Marta S, Silva L, Castro MA, Pezarat-Correia P, Cabri J (2012)** review, *J Electromyogr Kinesiol*
  22(6):803–813: “pectoralis major, subscapularis, and latissimus dorsi peaked during acceleration
  phase” — corroborates the above across the reviewed literature.
- **Side:** not explicitly separated in any accessible abstract; mechanistically the trail-side
  pectoralis major (internal rotation/horizontal adduction of the trail humerus) is the more heavily
  implicated side for acceleration/impact power in coaching/biomechanics secondary literature, but this
  is an inference, **not a directly cited lead/trail EMG split** — flagged.
- **Superseded by §1A:** a full 5-phase × 2-side %MMT grid was recovered on the second pass. Pectoralis
  major peaks at **93% MMT at acceleration**, the highest value recorded for any shoulder muscle in the
  swing, and is high on both sides (trail 12 → 64 → 93 → 74 → 37; lead 21 → 18 → 93 → 74 → 39). The
  trail side ramps earlier — 64% at forward swing vs the lead's 18% — so the *pattern* is trail-dominant
  through the downswing even where the acceleration peak is not. See §1A for the confidence caveat on the
  identical cross-side values.

### 2.2 Deltoid (anterior / middle / posterior)

- **Pink, Jobe, Perry 1990**: “anterior deltoid activates through forward swing and follow-through
  phases... middle and posterior deltoids showed minimal contribution” (reported directly as
  “relatively noncontributory”).
- **Jobe, Moynes, Antonelli 1986**: “the deltoid remained largely inactive on the right [trail] side” —
  i.e. for right-handed professional golfers, trail-side deltoid activity was low; by implication and
  cross-reference with Pink 1990's whole-muscle-group finding, deltoid overall (rotator-cuff-adjacent)
  is a low-activity muscle group in this swing relative to subscapularis/pec major/lat dorsi.
- **Superseded by §1A:** per-phase %MMT recovered for all three heads. Anterior deltoid peaks trail-side at
  forward swing (21%) and lead-side at late follow-through (26%) — a genuine side-by-phase inversion.
  Middle deltoid is 2–8% MMT across every phase; posterior deltoid 5–24% with no pattern. The
  "noncontributory" description is quantitatively confirmed for the middle and posterior heads.
- **Verdict:** anterior deltoid — low-to-moderate, active forward swing→follow-through; middle and
  posterior deltoid — low throughout, described explicitly as non-contributory. This is a directional/
  qualitative finding backed by a named primary source, not a quantified one.

### 2.3 Rotator cuff — supraspinatus, infraspinatus, subscapularis, teres minor

- **Jobe, Moynes, Antonelli 1986** (the rotator-cuff-specific paper): “the subscapularis was more active
  than any other muscle throughout the swing” (of the muscles studied). Deltoid inactive trail-side (see
  §2.2); latissimus dorsi and pectoralis major “provided power during acceleration.”
- **Pink, Jobe, Perry 1990**: “infraspinatus and supraspinatus act predominantly at the extremes of
  shoulder range of motion [i.e. top of backswing and end of follow-through], the subscapularis... during
  acceleration.”
- **Escamilla RF, Andrews JR (2009)** review, *Sports Med* 39(7):569–590: reports an aggregate **rotator
  cuff range of 28–68% MVIC** attributed to the golf swing context; this is a pooled range across the
  four rotator-cuff muscles and does not break out which muscle or phase produced the low vs high end —
  flagged as an aggregate, not a per-muscle figure.
- **Teres minor**: not separately reported as a distinct data point in any located source; it is
  presumably subsumed within the “rotator cuff” aggregate above in Escamilla's review, and was not one
  of the individually-named 8 muscles in the Pink 1990 / Jobe 1989 muscle set. **Not found as an
  individually reported golf-swing EMG value.**
- **Side:** Jobe 1986's finding that the deltoid (a non-cuff muscle in this context) was inactive
  specifically on the trail (right) side, combined with subscapularis being described as the single most
  active muscle "throughout the swing" (not restricted to one side in the abstract text available),
  suggests subscapularis activity is substantial bilaterally but the study population/emphasis (7 pro
  golfers) does not give a clean lead-vs-trail numeric split in the accessible text — flagged as a gap.
- **Superseded by §1A** for supraspinatus, infraspinatus and subscapularis: full per-phase, per-side %MMT
  recovered. The lead/trail split the abstracts could not give is stark in the numbers:
  - **Trail cuff fires early and goes quiet** — supraspinatus 25% and infraspinatus 27% at takeaway,
    falling to 7% and 9% by late follow-through.
  - **Lead cuff fires late** — infraspinatus 14% at takeaway rising to **61% at early follow-through**,
    the lead shoulder's decelerator. Lead supraspinatus peaks at 28%, also in follow-through.
  - **Subscapularis is the exception**: high on both sides throughout, trail-dominant (68% vs 41% at
    acceleration), confirming Jobe 1986's "more active than any other muscle throughout the swing"
    with numbers.
  - Escamilla's pooled 28–68% MVIC range brackets these values almost exactly (supraspinatus low end,
    subscapularis high end), an independent corroboration across normalisation methods.
- **Teres minor remains unmeasured** — it was not in the instrumented set, so §1A adds nothing for it.

### 2.4 Teres major

- **Not found in any golf-swing EMG study located this session.** Not part of the classic 8-muscle Pink/
  Jobe/Perry-lineage shoulder muscle set, and no independent study measuring it in golf was located.

### 2.5 Trapezius (upper / middle / lower)

- **Kao JT, Pink M, Jobe FW, Perry J (1995)**, *Am J Sports Med* 23(1):19–23 (15 competitive male
  golfers, bilateral EMG + cinematography, Kerlan-Jobe Orthopaedic Clinic): trapezius was one of the four
  scapular muscles studied (with rhomboids, levator scapulae, serratus anterior). Abstract text available
  states scapular muscles “work in synchrony” and that “trailing arm muscles stabilize during the
  swing” — no upper/middle/lower sub-division or numeric value recoverable from the accessible abstract.
- **Escamilla & Andrews 2009** review: “peak upper, middle and lower trapezius activity was **42–52%
  MVIC**” attributed to the golf-swing context — the only located numeric figure for trapezius in golf,
  and it is a pooled range across all three regions, not broken out individually, nor by phase or side.
- **Partly superseded by §1A:** McHardy's Table 3 gives **trail upper trapezius 52% MMT and trail middle
  trapezius 37% MMT at back swing**, and **lead middle trapezius 51% MMT at forward swing** — confirming
  Kao's qualitative trail-early / lead-late split with numbers. **Lower trapezius still has no recovered
  value at any phase.**

### 2.6 Rhomboids

- **Kao et al. 1995**: studied as one of the four scapular muscles; no numeric value recoverable from
  the accessible abstract.
- **Escamilla & Andrews 2009** review: “peak rhomboids activity was **approximately 60% MVIC**” in golf
  — single pooled peak figure, phase/side not specified.
- **Superseded by §1A:** McHardy's Table 3 gives **lead rhomboid 68% MMT at forward swing** — the single
  highest scapular value recorded on either side, and the lead side's most active muscle in that phase.
  This closely matches Escamilla's ~60% MVIC pooled peak. Trail rhomboid has no recovered number; Kao
  describes it retracting at takeaway then stabilising.
- Rhomboid major vs minor is not distinguished by any source.

### 2.7 Levator scapulae

- **Kao et al. 1995**: studied as one of the four scapular muscles; no numeric value recoverable from
  the accessible abstract.
- **Escamilla & Andrews 2009** review: “peak levator scapulae activity was **approximately 60% MVIC**”
  in golf — single pooled peak figure, phase/side not specified.
- **Superseded by §1A:** McHardy's Table 3 gives **lead levator scapulae 62% MMT at acceleration**, the
  lead side's second most active muscle in that phase — again close to Escamilla's ~60% MVIC pooled peak.
  Trail levator scapulae has no recovered number; Kao describes it elevating the scapula at takeaway then
  stabilising.

### 2.8 Serratus anterior

- **Kao et al. 1995**: “leading arm serratus anterior shows constant activity through all phases” —
  offered by the study as a candidate explanation for fatigue in high-volume golfers. This is the
  clearest **lead-vs-trail qualitative distinction** recovered for any scapular muscle in this pass:
  lead-side serratus anterior is described as continuously active across the whole swing, rather than
  phase-specific.
- **Escamilla & Andrews 2009** review: “peak serratus anterior activity was **approximately 70% MVIC**”
  in golf — the highest of the four scapular-muscle peak figures in that review, consistent with Kao's
  “constant activity” qualitative finding (sustained near-peak activity would read as a high peak value).
- **Superseded by §1A:** McHardy's Table 3 quantifies the trail side across three phases — **upper
  serratus 58% MMT at forward swing, 69% at acceleration** (the trail side's most active muscle in that
  phase), and **serratus anterior upper+lower 40% at late follow-through**. Lead upper serratus is
  **30% MMT at back swing**. Serratus is the highest-activity scapular muscle on both the %MMT and %MVIC
  scales, matching Escamilla's ~70% MVIC pooled peak.
- The upper vs lower digitation split implied by Table 3's differing labels ("upper serratus" in some
  cells, "upper + lower" in others) is not recoverable — Kao evidently instrumented them separately but
  the breakdown is in the paywalled full text.

### 2.9 Latissimus dorsi (shoulder role)

- **Jobe, Moynes, Antonelli 1986**: latissimus dorsi (with pectoralis major) “provided power during
  acceleration.”
- **Pink, Jobe, Perry 1990**: “latissimus dorsi [active] during forward swing.” (Note the minor
  cross-study discrepancy: Jobe 1986 ties lat dorsi to *acceleration*, Pink 1990 to *forward swing* — the
  two adjacent phases in the 5-phase scheme; both may be correct if activity ramps across the
  forward-swing→acceleration boundary, but no source explicitly reconciles the two statements.)
- **Marta et al. 2012** review: confirms latissimus dorsi (with pec major, subscapularis) “peaked during
  acceleration phase” across the reviewed literature — sides with the Jobe 1986 framing.
- **Numbers now exist — see [[07-verbatim-source-tables]].** Pink et al. 1990 per-phase %MMT:

  | Side | Takeaway | Forward swing | Acceleration | Early FT | Late FT |
  |---|---|---|---|---|---|
  | Trail (R) | 9 | **50** | 47 | 39 | 28 |
  | Lead (L) | 17 | **46** | 31 | 32 | 18 |

  Peak is **forward swing bilaterally**, trail slightly higher than lead throughout the downswing.
  **Single-source caveat:** latissimus never appears in McHardy Table 3, so unlike the other nine muscle
  rows this one could not be independently cross-validated.
- The peak-phase dispute is now **three-way**: Pink 1990 says forward swing; Kim et al. 2004 says
  downswing and acceleration; Marta et al. 2012 says acceleration. Plausibly a phase-boundary artefact —
  Pink's "forward swing" *is* the early downswing, which is Kim's "downswing" column — but the sources
  differ as printed. Report the range.
- The nearest numeric anchor is **Pezarat-Correia et al. 2006**, which recorded trail-side latissimus
  dorsi at **53% MVC — the highest of the 12 dominant-arm muscles it measured** — but with n=3 and a
  3-phase scheme, so it fixes magnitude only loosely and cannot settle the phase question.

---

## 3. Arm muscles

### 3.1 Biceps brachii

- Not part of the classic Pink/Jobe/Perry 8-shoulder-muscle set; not covered by Farber et al. 2009
  (forearm study) or Glazebrook et al. 1994 (wrist study, elbow-flexor-adjacent but did not include
  biceps).
- **Bochnia JM, Bockholt S, Gosheger G, Theil C, Schneider KN (2024)**, *BMC Musculoskelet Disord*
  25(1):668 (PMC11346012; 30 right-handed amateur + professional golfers, surface EMG, standard grip
  condition, raw µV, **not %MVC** — see §0): biceps brachii mean activity by phase (Jobe 5-phase scheme):

  | Phase | Lead arm (µV) | Trail arm (µV) |
  |---|---|---|
  | Takeaway | 13.9 | 40.1 |
  | Forward swing | 21.6 | 38.2 |
  | Acceleration | 34.9 | 41.7 |
  | Early follow-through | 77.8 | 66.8 |
  | Late follow-through | 155.7 | 125.7 |

  Pattern (valid only as a within-study relative shape, per §0): both arms show a monotonic rise from
  Takeaway through Late follow-through, with the steepest increase after impact — consistent with biceps
  brachii's role decelerating/controlling elbow extension and arresting the club's momentum through
  release and the follow-through, rather than generating power in the downswing. Lead arm shows the
  higher absolute late-follow-through reading in this raw-µV dataset; not necessarily true in normalised
  %MVC terms (see §0 caveat).
- Same pattern (biceps brachii present, raw µV, standard grip) reconfirmed directionally in **Grieß et
  al. (2026)**, *BMC Musculoskelet Disord* (PMC12930853; steel vs graphite shaft study), though the
  extracted text for that paper focused on FCU/pronator teres late-follow-through comparisons and did not
  surface a full biceps table this session.
- **Correction to the first pass:** one true %MVC value does exist — **Pezarat-Correia et al. 2006**
  (n=3, trail arm only, 3-phase scheme) reports trail-arm **biceps brachii 26% MVC, peaking in the
  backswing**, grouped with brachioradialis (45%) as elbow flexors "silenced before the DS initiation".
- **This directly contradicts the Bochnia/Grieß µV data above**, which show biceps rising monotonically to
  a peak in **late follow-through** on both sides (e.g. Bochnia lead arm: 13.9 → 21.6 → 34.9 → 77.8 →
  155.7 µV). Backswing peak vs late-follow-through peak is not a small discrepancy.
- The conflict is **unresolved and confounded**: %MVC vs raw µV, n=3 vs n=30/40, 3-phase vs 5-phase
  binning, trail-only vs bilateral. A 3-phase scheme pools much more of the swing into each bin, which
  could plausibly relocate an apparent peak. Do not silently pick one; the app should treat biceps
  peak-phase as low-confidence.

### 3.2 Triceps brachii

- **Correction to the first pass, which recorded this muscle as having no golf data.** A golf-specific
  value does exist for the **trail arm**: **Pezarat-Correia P, Cabri J, Fernandes O, Sousa JP (2006)**,
  "Electromyographic Analysis of the Dominant Upper Limb During the Golf Swing," *Proc ECSS Lausanne*
  3(1):70–85 — trail-arm **triceps brachii long head 50% MVC, peaking in the downswing**. This was the
  second-highest of the 12 dominant-arm muscles that study recorded, behind only latissimus dorsi (53%).
  The paper states elbow extensors "presented the highest EMG activation" during the downswing and are
  "activated at the beginning of the DS".
- Caveats: **n=3 low-handicap golfers, pitch iron, 3-phase scheme (backswing/downswing/follow-through),
  trail arm only.** Conference proceedings, not a peer-reviewed journal article. Treat as indicative of
  magnitude and phase, not as an established value.
- **Lead-arm triceps brachii remains genuinely unmeasured.** Biomechanically the lead elbow must resist
  flexion torque from the top of the backswing through impact, implying sustained activity, but no source
  quantifies it. Do not assign the trail-arm figure to the lead arm.
- Escamilla & Andrews 2009 covers triceps for upper-extremity sports generally but gives no golf-specific
  figure.

### 3.3 Brachioradialis

- **Correction to the first pass, which recorded this muscle as having no golf data.** Correct that it is
  absent from the Farber et al. 2009 four-muscle forearm set (FCR, pronator teres, FCU, ECRB), the
  Glazebrook et al. 1994 wrist study, and the Bochnia/Grieß four-muscle set (ECRB, FCU, pronator teres,
  biceps brachii) — but **Pezarat-Correia et al. 2006 did measure it**: trail-arm **brachioradialis
  45% MVC, peaking in the backswing**. That is the highest elbow-flexor value reported anywhere in the
  golf EMG literature. The paper groups it with biceps as elbow flexors showing "strongest activation
  during the BS to promote elbow flexion and hand extension, and silenced before the DS initiation".
- Same caveats as §3.2: n=3, trail arm only, 3-phase scheme, conference proceedings.
- **Lead-arm brachioradialis has no EMG data.** The only lead-side evidence is a clinical case report —
  Nakamura G, Abe M, Kumano H, *J Hand Surg Asian Pac Vol* 2019 — of acute compartment syndrome from a
  haematoma within the **lead** forearm's brachioradialis sustained while playing golf (radial
  compartment pressure 120 mmHg). That establishes the muscle is mechanically loaded enough in the swing
  to be an injury site, but it is not activation data.

### 3.4 Pronator teres

- **Farber AJ, Smith JS, Kvitne RS, Mohr KJ, Shin SS (2009)**, *Am J Sports Med* 37(2):396–401 (10 male
  amateur + 10 male professional right-handed golfers, fine-wire EMG, values as **% of maximal manual
  muscle test** — see §0 methodology warning, not true %MVC):

  | Phase | Side | Amateur | Professional | Significance |
  |---|---|---|---|---|
  | Forward swing | Trail | **120.9%** | 57.4% | p = .04 |
  | Acceleration | Trail | 104.8% | 53.1% | p = .08 (trend) |
  | Acceleration | Lead | 36.3% | **88.1%** | p = .03 |
  | Early follow-through | Lead | 28.8% | 58.1% | p = .06 (trend) |

  Direction of the skill effect **reverses by side**: amateurs over-activate trail-arm pronator teres
  during forward swing/acceleration (linked by the authors to medial-epicondylitis risk); professionals
  show *greater* lead-arm pronator teres activity during acceleration/early follow-through. Conclusion
  stated directly by the authors: “pronator teres muscle activity in the golf swing differs significantly
  between professional and amateur golfers,” with a clinical recommendation toward pronator teres
  stretching/strengthening for amateurs.
- **Bochnia et al. 2024** (raw µV, standard grip, both skill levels pooled):

  | Phase | Lead (µV) | Trail (µV) |
  |---|---|---|
  | Takeaway | 58.1 | 48.6 |
  | Forward swing | 51.7 | 39.3 |
  | Acceleration | 54.2 | 41.3 |
  | Early follow-through | 88.3 | 91.3 |
  | Late follow-through | 124.0 | 105.1 |

  Same late-swing rise pattern as biceps brachii (§3.1); values not comparable in magnitude to the
  Farber %MMT figures (different normalisation — see §0).
- **Grieß et al. (2026)** (steel vs graphite shaft): lead-arm pronator teres, late follow-through, steel
  166.09 µV vs graphite 155.00 µV (p = 0.009, statistically significant reduction with graphite shaft);
  trail-arm PT late follow-through also higher with steel in the elbow-pain-free subgroup (p = 0.032).
  Confirms late follow-through as the phase of peak raw-amplitude pronator teres activity in this raw-µV
  dataset, consistent with Bochnia's table above.

### 3.5 Supinator

- **Not found in any golf-swing EMG study located this session.**

---

## 4. Forearm, wrist and hand

### 4.1 Wrist flexor group (flexor carpi radialis, flexor carpi ulnaris, flexor digitorum superficialis/profundus)

- **Glazebrook MA, Curwin S, Islam MN, Kozey J, Stanish WD (1994)**, *Am J Sports Med* 22(5):674–679
  (medial epicondylitis / golfer's elbow study; true **%MVC**, own 4-phase scheme including a distinct
  Address timepoint — see §1):
  - Flexor muscles: “a consistent burst of electromyographic activity during contact [impact] phase
    (flexor burst, **90.77% of MVC**).”
  - **Symptomatic (medial-epicondylitis) golfers showed significantly greater mean flexor EMG activity
    than asymptomatic golfers, both at address and across the swing phases** — direct, quoted finding
    from the abstract, and the paper's central clinical result.
  - Address-to-contact numeric progression is given explicitly for the **extensor** group (§4.2), not
    quoted with the same address→contact range for flexors in the accessible abstract — only the single
    peak 90.77% figure at contact is recoverable for flexors.
  - Side (lead vs trail) not distinguished in the accessible abstract text.
- **Farber et al. 2009**: flexor carpi radialis and flexor carpi ulnaris were two of the four muscles
  fine-wire-tested, but **no numeric values for either muscle were recoverable from any accessible
  source** — the study's abstract and every secondary summary found report pronator teres numbers only
  (§3.4); FCR/FCU results exist in the paywalled full text but were not accessible this session.
- **Bochnia et al. 2024** (raw µV, standard grip, FCU only — FCR/FDS/FDP not part of this study's muscle
  set):

  | Phase | Lead FCU (µV) | Trail FCU (µV) |
  |---|---|---|
  | Takeaway | 76.6 | 61.2 |
  | Forward swing | 123.0 | 68.7 |
  | Acceleration | 115.4 | 107.0 |
  | Early follow-through | 138.5 | **201.4** |
  | Late follow-through | 120.2 | 158.0 |

  Trail FCU shows a marked spike at early follow-through (immediately post-impact) relative to lead FCU
  in this raw-µV dataset — directionally consistent with the trail wrist's rapid flexor-driven release/
  roll-over through impact, though (per §0) this is a within-study relative pattern, not a normalised
  %MVC comparison.
- **Grieß et al. 2026**: lead-arm FCU, late follow-through, steel 158.17 µV vs graphite 150.67 µV (p =
  0.027) — small but statistically significant shaft-material effect, same phase/side as the pronator
  teres finding in §3.4.
- **FDS/FDP (flexor digitorum superficialis/profundus): not found in any golf-swing EMG study located
  this session.**

### 4.2 Wrist extensor group (ECRL, ECRB, ECU, extensor digitorum)

- **Glazebrook et al. 1994**: “extensor [activity was] persistent throughout the four swing phases,
  ranging from **33.59% of MVC at address to 58.77% at contact** [impact].” This is the clearest
  address-to-impact numeric progression recovered for any forearm muscle group in true %MVC terms.
- **Bochnia et al. 2024** (raw µV, standard grip, ECRB):

  | Phase | Lead ECRB (µV) | Trail ECRB (µV) |
  |---|---|---|
  | Takeaway | 65.3 | **98.5** |
  | Forward swing | 48.2 | 84.0 |
  | Acceleration | 55.0 | 48.4 |
  | Early follow-through | 142.2 | 60.4 |
  | Late follow-through | 130.6 | 129.8 |

  Trail ECRB peaks early (Takeaway, i.e. backswing) then falls; lead ECRB is comparatively low through
  the backswing/downswing and spikes sharply at early follow-through — an inverse lead/trail timing
  pattern (again, relative/within-study only per §0).
- **Robinson PG, Carson HJ, Richards J, Murray A, Duckworth AD, Campbell D (2023)**, *J Sports Sci*
  41(17):1596–1604 (15 sub-elite male golfers, surface EMG on extensor carpi ulnaris specifically,
  pitching wedge/7-iron/driver): **statistically greater trail-ECU recruitment during the downswing (p <
  0.001) across all clubs; lead-ECU recruitment greater during backswing (p < 0.001) and follow-through
  (p < 0.024)**. No absolute %MVC value reported — significance/direction only. Authors link the
  asymmetric lead/trail wrist kinematics and muscle activity pattern to golf's clinically asymmetric
  injury pattern (i.e. why lead- and trail-wrist overuse injuries differ in golfers). No significant
  relationship found between downswing ECU EMG and clubhead-speed kinematics at impact.
- **Grieß et al. 2026**: trail-arm FCU with overlap grip showed higher activity with steel shaft during
  forward swing (p = 0.021) — an ECU-adjacent forearm finding from the same dataset family, included
  here for completeness though it is FCU not ECU.
- **Extensor digitorum / ECRL specifically: not found as individually reported golf-swing EMG values** —
  only ECRB (Bochnia/Grieß) and ECU (Robinson) are individually named in accessible sources; Glazebrook's
  90.77%/33.59–58.77% figures are for “extensor muscles”/“flexor muscles” as pooled groups, not named
  individual muscles.

### 4.3 Intrinsic hand / grip muscles

- **Not found in any golf-swing EMG study located this session.** No source measuring first dorsal
  interosseous, thenar, or hypothenar muscle activity during the golf swing was located. Grip-related
  measurement in the literature is via **force/pressure sensors** on the club or glove (§6), not
  intrinsic-hand EMG.

---

## 5. Which muscles peak, and in which phase (summary)

Compiled from the sources above; “phase” uses each source's own terminology per §1.

Side attributions for the shoulder and scapular rows were filled in on the second pass from §1A; rows
previously marked "not separated" now carry the measured %MMT peak.

| Muscle | Reported peak phase | Side (if specified) | Source |
|---|---|---|---|
| Subscapularis | Acceleration; high throughout, most active cuff muscle overall | **Trail 68%**, lead 41% | Jobe 1986; Pink 1990 |
| Pectoralis major | Acceleration — highest shoulder value in the swing | **Both 93%**; trail ramps earlier (64% vs 18% at forward swing) | Pink 1990; Marta 2012 |
| Latissimus dorsi | Forward swing (Pink 1990) / Acceleration (Jobe 1986, Marta 2012) — adjacent-phase discrepancy, not reconciled | Not separated; no %MMT value | Jobe 1986; Pink 1990; Marta 2012 |
| Anterior deltoid | Trail: forward swing (21%). Lead: late follow-through (26%) | **Side-inverted** | Pink 1990 |
| Middle deltoid | No peak — 2–8% MMT throughout | Both | Pink 1990 |
| Posterior deltoid | No peak — 5–24% MMT, no pattern | Both | Pink 1990 |
| Supraspinatus | Trail: takeaway (25%). Lead: early/late follow-through (28%) | **Side-inverted** | Pink 1990 |
| Infraspinatus | Trail: takeaway (27%). Lead: early follow-through (**61%**) | **Side-inverted, large lead peak** | Pink 1990 |
| Upper trapezius | Back swing (**52%**) | **Trail** | Kao 1995 via McHardy 2005 |
| Middle trapezius | Trail: back swing (37%). Lead: forward swing (51%) | **Side-inverted** | Kao 1995 via McHardy 2005 |
| Lower trapezius | No numeric value recovered at any phase | — | — |
| Rhomboids | Forward swing (**68%** — highest scapular value) | **Lead** | Kao 1995 via McHardy 2005 |
| Levator scapulae | Acceleration (62%) | **Lead** | Kao 1995 via McHardy 2005 |
| Serratus anterior | Trail: acceleration (**69%**). Lead: constant/sustained across all phases (30% at back swing) | Both, differing patterns | Kao 1995; McHardy 2005 |
| Triceps brachii (long head) | Downswing (50% MVC) | **Trail only**; lead unmeasured | Pezarat-Correia 2006, n=3 |
| Brachioradialis | Backswing (45% MVC) | **Trail only**; lead unmeasured | Pezarat-Correia 2006, n=3 |
| Biceps brachii | Backswing (26% MVC, Pezarat-Correia) **vs** late follow-through (raw µV, Bochnia/Grieß) — unresolved conflict | Trail (Pezarat); both (Bochnia) | See §3.1 |
| Wrist extensors (pooled) | Rising address → contact, peak at contact/impact | Not separated | Glazebrook 1994 |
| Wrist flexors (pooled) | Burst at contact/impact | Not separated | Glazebrook 1994 |
| ECU | Downswing | **Trail** peak | Robinson 2023 |
| ECU | Backswing and follow-through | **Lead** peak | Robinson 2023 |
| ECRB (raw amplitude) | Takeaway (backswing) | **Trail** | Bochnia 2024 |
| ECRB (raw amplitude) | Early follow-through | **Lead** | Bochnia 2024 |
| Pronator teres (professionals) | Acceleration | **Lead** | Farber 2009 |
| Pronator teres (amateurs) | Forward swing | **Trail** | Farber 2009 |
| Pronator teres / FCU / biceps brachii (raw amplitude, all sides) | Late follow-through | Both, lead numerically higher in Bochnia's biceps data | Bochnia 2024; Grieß 2026 |

**Read this table as directional** — muscles still absent from it (teres minor, teres major, supinator,
lower trapezius, lead-arm triceps and brachioradialis, intrinsic hand muscles) have **no** phase-of-peak
data, per §§2–4 and §10.

**The single most important structural finding for the app**: the trail side peaks *early* (takeaway/
backswing) and the lead side peaks *late* (follow-through) for supraspinatus, infraspinatus, middle
trapezius, anterior deltoid and ECRB alike. This side-inverted timing is the dominant organising pattern
of the upper limb in the swing — the trail side positions and drives, the lead side stabilises then
decelerates. Subscapularis and pectoralis major are the exceptions: both peak at acceleration on both
sides.

**"Peak near impact" is not a universal rule.** It holds for the pooled wrist flexors and extensors
(Glazebrook, at contact) and for trail ECU (downswing), but Robinson 2023 puts lead ECU's peaks in
backswing and follow-through, and the two large raw-µV studies put most muscle/side combinations' peak in
**late follow-through**. Model peak phase per muscle and per side, never as one global rule.

---

## 6. Grip force through the swing

- **Langlais SM, Broker JP (2014)**, *Sports Biomech* 13(2):109–122 (8 low-handicap golfers, USGA index
  0–7, own 7-iron and driver, grip-mounted force sensors, comparing anatomically specific force
  “signatures”):
  - “Dominant forces arose primarily from the lead hand, specifically the last three fingers.”
  - Within-swing force variability was **greatest during club acceleration** and **dramatically decreased
    at impact** — i.e. grip-force *timing/pattern* becomes highly repeatable right at impact even though
    absolute forces are changing rapidly.
  - Force-profile repeatability across swings for a given golfer: standard deviation **<7% of total
    force**.
  - Force-profile correlation between 7-iron and driver for the same golfer: **r² = 0.86** — a golfer's
    grip-force “signature” is largely club-invariant in shape, even though (per the paper's stated
    purpose) absolute magnitudes/timing differ between clubs.
  - **No absolute force values (N or kg) at specific swing phases were recoverable from the accessible
    abstract** — only variability/correlation statistics. Full-text (with the actual force curves) was
    not accessible this session.
- **Koike S, Shiraki H, Fujii N, Ae M (2005)**, “Kinetic Analysis of Each Hand During Golf Swing with Use
  of an Instrumented Golf Club,” *Proceedings of the ISB XXth Congress / ASB 29th Annual Meeting*,
  Cleveland, OH, p. 515 (primary source, directly read; strain-gauge instrumented grip handle, VICON
  motion capture at 250 Hz, force/moment sampling at 500 Hz; **2 professional golfers**, driver/5-iron/
  sand wedge):
  - Reports hand forces along the grip's long axis (y-axis of a swing-plane-relative coordinate system)
    for the 5-iron, normalised time 0% (start of forward/downswing) → 100% (impact).
  - **Head-side (lead) hand**: axial force roughly constant to ~70% of normalised downswing time, then
    rises sharply, reaching a peak at approximately **90%** of normalised time, and **holds near that peak
    through impact**.
  - **Grip-end-side (trail) hand**: a different pattern — force increases gradually only from ~80% of
    normalised time through to impact.
  - **Resultant (combined) force increases gradually toward impact**, attributed by the authors to rising
    centrifugal force on the club.
  - Graph axes (read directly from the paper's Figure 2, not a table — approximate) span roughly **−300 N
    to +400 N** for the individual-hand axial force components; precise values were not given in text,
    only in the figure. **Treat as approximate, graph-read, small-sample (n = 2) data**, not a precision
    benchmark.
  - Authors explicitly note that “the kinetic responses of the two players showed considerably different
    patterns” between clubs — i.e. this study itself cautions against generalising its exact curve
    shape/magnitude beyond its two subjects.
- **Schmidt ER (2007)**, PhD thesis, Loughborough University, “Measurement of grip force and evaluation
  of its role in a golf shot” — **only accessed via secondary citation on a golf-instruction website
  (tutelman.com), not independently verified against the primary thesis this session; treat the following
  as lower-confidence, secondary-sourced figures:**
  - Glove-mounted pressure sensors, professional golfer: near-impact total grip force **≈160 N (≈36
    lb)**; trail-hand contribution near impact **≈5%** of total force (implying strongly lead-hand-
    dominant loading, consistent with Langlais & Broker's finding above).
  - Grip(handle)-mounted sensors, 6-handicap amateur: **≈500 N (≈113 lb) at impact** — roughly 3.2× higher
    than the glove-sensor reading, which the secondary source attributes to a systematic difference
    between glove-based and handle-based sensing methods rather than a true golfer-to-golfer difference.
    **This means absolute grip-force magnitude is highly sensor-method-dependent** — do not treat either
    number as a general physiological constant.
- **Additional Langlais & Broker detail recovered on the second pass** (same paper as above):
  - **Trail-hand force is substantially lower than lead-hand throughout the swing — except at takeaway**,
    where the two are similar. The trail hand contributes proportionally most early, then falls away.
  - **4 of 8 golfers showed a distinct trail index-finger pressure spike (~20% of total force)
    immediately pre-impact.** Present in only half the sample, so not a universal feature.
  - The r²=0.86 cross-club correlation splits by hand: **lead hand r²=0.90, trail hand r²=0.73** — the
    lead hand's grip signature is markedly more club-invariant than the trail hand's.
  - 7-iron coefficient of variation at impact ≈5%.
- **Choi H, Park S (2020)**, “Three Dimensional Upper Limb Joint Kinetics of a Golf Swing with Measured
  Internal Grip Force,” *Sensors* 20(13):3672, PMID 32630024 (9 professional males, driver, custom
  axially-separated grip with an embedded 6-axis force/torque sensor):
  - **Trail-hand torque is roughly threefold greater than lead-hand torque.** This is the key
    counterweight to the "lead hand dominates" finding above — the lead hand supplies more *linear grip
    force*, the trail hand more *rotational torque*. Different mechanical quantities; **do not merge them
    into one "grip strength" number.**
  - Both hands exert simultaneous opposing counterforces against each other throughout the swing.
  - **Lead-arm joint force/torque onset and peak precede the trail arm's by roughly 50–200 ms**;
    trail-arm peaks cluster around impact and are larger in magnitude. This is a directly measured
    lead-then-trail sequencing, useful for the app's timing model.
  - Downswing shows backward/upward torque followed by an abrupt reversal around impact.
  - Data presented graphically; **no absolute Newton values extractable from the text.**
- **Budney DR (1979)**, “Measuring grip pressure during the golf swing,” *Res Q* 50(2):272–277,
  PMID 472468 — the earliest grip-pressure study. **PubMed holds no abstract and no open-access full text
  was reachable.** Numeric values, phase breakdown and lead/trail comparison could not be retrieved.
  Recorded here so the citation is not lost, but it contributes no usable data.
- **Whether grip pressure "spikes" at impact is not settled.** Langlais & Broker report variability
  peaking during acceleration and *collapsing* at impact — a convergence toward a repeatable pattern, not
  necessarily a magnitude spike — while Koike's lead-hand curve peaks at ~90% of downswing time and holds
  through impact, and the trail-hand index spike appears in only half of Langlais's sample. The app should
  not animate a universal sharp grip spike at impact as though it were established.
- **Qualitative consensus across the grip-force sources**: force is low and relatively stable
  during the backswing/takeaway, becomes highly variable during the downswing/acceleration as the golfer
  actively manipulates the club, then rises toward a peak at or immediately before impact, with the
  **lead hand supplying the dominant share of grip force throughout**, especially near impact. No source
  gave a single, precise, high-confidence address-to-impact numeric curve in absolute units (N or kg) —
  this remains a **genuine data gap** for the app's grip-force-over-time model; the Koike figures are the
  best directly-verified approximation, with the important caveat of n = 2.

---

## 7. Lead vs trail — summarised

- **Wrist/forearm (best-evidenced asymmetry in this pass):**
  - ECU: trail peaks in the downswing; lead peaks in backswing and follow-through (Robinson 2023, p <
    0.001/0.024).
  - ECRB (raw amplitude): trail peaks early (backswing/takeaway); lead peaks late (early follow-through)
    (Bochnia 2024) — same inverse-timing shape as ECU.
  - FCU (raw amplitude): trail shows a sharp early-follow-through spike (immediately post-impact) not
    mirrored as strongly in lead FCU (Bochnia 2024).
  - Pronator teres: skill-dependent, side-reversing pattern — amateurs over-activate **trail** PT in
    forward swing/acceleration; professionals show relatively more **lead** PT activity in
    acceleration/early follow-through (Farber 2009, both p < .05).
  - Net picture: the **trail forearm drives the downswing/release**, the **lead forearm stabilises through
    backswing and controls/decelerates through follow-through** — consistent across three independent
    forearm datasets (Robinson, Bochnia, Farber), though none of the three use the same normalisation
    convention (§0), so the *shape* of the asymmetry is well corroborated while the *magnitude* is not
    cross-comparable.
- **Shoulder — now quantified per side via §1A** (this supersedes the first pass's note that no source
  separated lead from trail):
  - **Rotator cuff is starkly side-inverted.** Trail supraspinatus (25%) and infraspinatus (27%) peak at
    takeaway then fall to 7–9% by late follow-through. Lead infraspinatus does the opposite — 14% at
    takeaway rising to **61% at early follow-through**, the lead shoulder acting as the decelerator.
    Lead supraspinatus likewise peaks late (28%).
  - **Subscapularis is trail-dominant and always on** — 68% vs 41% at acceleration, higher on the trail
    side in every phase after takeaway. Confirms Jobe 1986's "more active than any other muscle
    throughout the swing" with numbers.
  - **Pectoralis major is the exception to the asymmetry**: 93% MMT on *both* sides at acceleration. The
    asymmetry is in timing, not peak — trail 64% vs lead 18% at forward swing. (See §1A's flagged
    caveat on the identical cross-side values.)
  - **Anterior deltoid is side-inverted**: trail peaks at forward swing (21%), lead at late
    follow-through (26%). Middle (2–8%) and posterior (5–24%) deltoid are quantitatively confirmed as
    non-contributory on both sides.
  - **Scapular muscles split cleanly by phase**: trail peaks at back swing (upper trapezius 52%, middle
    trapezius 37%, plus rhomboids and levator scapulae retracting/elevating per Kao); lead peaks through
    forward swing and acceleration (rhomboid 68%, middle trapezius 51%, levator scapulae 62%).
  - **Lead serratus anterior is the outlier — constant activity across all phases** (Kao 1995), which Kao
    links to fatigue in high-volume golfers. Trail serratus peaks at acceleration (69%).
  - **Latissimus dorsi remains the one shoulder muscle with no per-side quantification** — do not assume
    trail-dominance for it.
  - **Injury laterality corroborates the asymmetry**: over 90% of golfers' shoulder problems involve the
    lead shoulder, and lead-shoulder injuries are roughly 3× as common as trail (Kim, Millett, Warner &
    Jobe 2004) — consistent with the lead cuff absorbing the deceleration load.
- **Grip force — the two hands do different jobs:**
  - **Lead hand supplies the dominant share of linear grip force** throughout the swing, especially the
    last three fingers (Langlais & Broker 2014; lower-confidence Schmidt 2007). Trail-hand force is
    substantially lower except at takeaway, where the two are similar.
  - **Trail hand supplies roughly threefold more torque** (Choi & Park 2020). Force and torque are
    different mechanical quantities from different studies — **do not merge into a single "grip
    strength" curve.**
  - **Lead-arm joint force/torque leads the trail arm by ~50–200 ms**, with trail-arm peaks clustering
    around impact at larger magnitude (Choi & Park 2020) — a measured lead-then-trail sequencing.
  - The lead hand's grip signature is far more club-invariant than the trail hand's (r²=0.90 vs 0.73,
    Langlais & Broker 2014).

---

## 8. Typical %MVC magnitude bands

Only a partial picture is available, since most of the classic shoulder/scapular papers report
qualitative activity patterns rather than numeric bands in their accessible abstracts. Bands recoverable
this session, **explicitly labelled by source and normalisation type**:

| Band | Muscle(s) | Value | Source / convention |
|---|---|---|---|
| High | Rotator cuff (pooled) | 28–68% MVIC | Escamilla & Andrews 2009 review |
| High | Serratus anterior | ~70% MVIC | Escamilla & Andrews 2009 review |
| Moderate–high | Rhomboids | ~60% MVIC | Escamilla & Andrews 2009 review |
| Moderate–high | Levator scapulae | ~60% MVIC | Escamilla & Andrews 2009 review |
| Moderate | Trapezius (upper/mid/lower pooled) | 42–52% MVIC | Escamilla & Andrews 2009 review |
| Moderate → very high | Wrist extensors (pooled) | 33.59% MVC (address) → 58.77% MVC (contact) | Glazebrook 1994, true %MVC |
| Very high (burst) | Wrist flexors (pooled) | 90.77% MVC at contact | Glazebrook 1994, true %MVC |
| Exceeds 100% (methodology-specific) | Pronator teres | 28.8%–120.9% depending on phase/side/skill | Farber 2009, **%MMT not %MVC** — see §0, not directly comparable to the MVIC/MVC rows above |
| General literature statement | Forearm muscles broadly | “activity levels above the maximal voluntary contraction” reported in some reviewed studies | Marta et al. 2012 review — corroborates that forearm muscles routinely exceed nominal 100% reference values in this literature, whichever reference contraction is used |

**Updated on the second pass** — bands now recoverable for muscles previously listed as having none
(all **%MMT**, Pink 1990 via §1A; not comparable to the %MVIC/%MVC rows above):

| Band | Muscle | Value | Source |
|---|---|---|---|
| Very high | Pectoralis major | 93% MMT peak (acceleration, both sides) | Pink 1990 |
| High | Subscapularis | 68% MMT peak (trail, acceleration); 41% lead | Pink 1990 |
| High | Infraspinatus (lead) | 61% MMT peak (early follow-through) | Pink 1990 |
| Low–moderate | Supraspinatus | 7–28% MMT across all phases/sides | Pink 1990 |
| Low–moderate | Infraspinatus (trail) | 7–27% MMT | Pink 1990 |
| Low–moderate | Anterior deltoid | 5–26% MMT | Pink 1990 |
| Low | Middle deltoid | 2–8% MMT, all phases, both sides | Pink 1990 |
| Low | Posterior deltoid | 5–24% MMT, no pattern | Pink 1990 |
| High | Trail triceps long head | 50% MVC (downswing) | Pezarat-Correia 2006, n=3 |
| Moderate–high | Trail brachioradialis | 45% MVC (backswing) | Pezarat-Correia 2006, n=3 |
| Moderate | Trail biceps brachii | 26% MVC (backswing) | Pezarat-Correia 2006, n=3 |
| High | Trail latissimus dorsi | 53% MVC | Pezarat-Correia 2006, n=3 |

**Still no band for**: teres minor, teres major, supinator, lower trapezius, lead-arm triceps and
brachioradialis, individually-named wrist flexors/extensors beyond the pooled Glazebrook figures, and
intrinsic hand muscles.

**The commonly-quoted four-tier scheme (<20% low / 20–40% moderate / 40–60% high / >60% very high) could
not be traced to any golf EMG paper.** What the golf literature actually does: Pink, Perry & Jobe 1993
uses a **binary** cutoff at **30% MMT** ("relatively low" below, "relatively high" above); Glazebrook 1994
reports raw percentages with no bands; Kao 1995, Marta 2012 and McHardy & Pollard 2005 use purely
qualitative words with no numeric cutoffs. If the app implements a four-tier band, attribute it to general
sports-EMG convention, **not** to any golf source.

**Values above 100% are real and must not be clamped.** Farber 2009's amateur trail pronator teres reads
120.9% MMT, and Marta et al. 2012 notes wrist flexor activity "above the maximal voluntary contraction".
Dynamic ballistic EMG routinely exceeds a static isometric or manual-test reference. A colour mapping that
saturates at 100% would silently truncate the single highest-activation muscle in the swing.

---

## 9. Professional vs amateur differences

- **Pronator teres is the single most clearly evidenced skill-level difference** in this pass (Farber
  2009, §3.4): amateurs over-activate trail-arm PT during forward swing and acceleration (linked to
  medial-epicondylitis/golfer's-elbow risk by the authors); professionals show comparatively greater
  lead-arm PT activity during acceleration and early follow-through. The direction of the professional-
  vs-amateur difference **reverses depending on which arm** — a genuinely nuanced finding, not a simple
  “pros use more/less muscle” statement.
- **Shoulder (gender comparison, not skill level, but same research lineage):** Jobe FW, Perry J, Pink M
  (1989), *Am J Sports Med* 17(6):782–787 (8 shoulder muscles, professional golfers only): women showed
  slightly more activity during takeaway/forward swing; men showed slightly more during
  acceleration/follow-through; differences were **not statistically significant** (independent t-tests, P
  = 0.05). This is a men-vs-women-professionals comparison, not professional-vs-amateur — included here
  because it is the only other located skill/demographic EMG comparison in the shoulder-girdle
  literature, and should not be conflated with a skill-level finding.
- **Grip pressure/ergonomics (indirect skill-adjacent evidence):** Bochnia et al. 2024 note their
  ergonomic-grip effect was more pronounced “for amateur golfers with fewer than 20 weekly playing
  hours” — a practice-volume rather than strict skill-level split, but directionally consistent with
  lower-practice golfers showing more forearm-muscle-activity change from an equipment intervention.
- **General injury-epidemiology framing (not EMG, but relevant context):** McHardy A, Pollard H, Luo K
  (2006), *Sports Med* 36(2):171–187: overuse injuries are more prevalent among professionals, while
  traumatic/technique-related injuries are more common among amateurs — a plausible downstream
  consequence of the volume/repetition difference between the two groups rather than a direct EMG finding.
- **Sorbie GG, Hunter HH, Grace FM, Gu Y, Baker JS, Ugbolue UC (2016)**, *Res Sports Med*, PMID 27267082
  (15 right-handed males, ECRB and flexor digitorum superficialis, lead and trail, three grip sizes,
  7-iron): **amateurs produced significantly greater forearm muscle activity than professionals during
  both backswing and downswing, across all three grip sizes (p<0.05).** Grip size itself had no
  significant effect on muscle activity. Absolute values are not in the accessible abstract.
  - This is a **second, independent** skill-level forearm finding beyond Farber 2009, and it points the
    same way: **amateurs work the forearm harder and earlier.** Together the two studies support a
    general pattern of amateurs over-recruiting the forearm, with professionals recruiting later, more
    selectively, and more on the lead side.
- **Sorbie GG, Darroch P, Grace FM, Gu Y, Baker JS, Ugbolue UC (2017)**, *Res Sports Med*, PMID 28819996:
  no significant forearm EMG difference between gloved and ungloved conditions, despite a clubhead-speed
  benefit with driver-plus-glove.
- **No professional-vs-amateur numeric comparison was located for any shoulder-girdle muscle** (pec
  major, deltoid, rotator cuff, scapular muscles, lat dorsi) — the only quantified pro-vs-amateur
  contrasts recovered are the forearm datasets (Farber 2009 pronator teres, Sorbie 2016 ECRB/FDS).
  Marta et al. 2012 states the gap directly: "there is a lack of studies on average golf players, since
  most studies were executed on professional or low handicap golfers."

---

## 10. What could not be verified — explicit gaps

- **RESOLVED on the second pass, for Pink 1990 and partially for Kao 1995 — see §1A.** A full 5-phase ×
  2-side %MMT grid was recovered for the eight Pink 1990 shoulder muscles, and peak-cell %MMT values for
  the scapular muscles via McHardy & Pollard 2005 Table 3. The first pass's statement that no numeric
  table was recoverable is superseded. What remains outstanding from the classic papers:
  - **Kao 1995's full per-phase scapular grid** — only the peak cells that surface in McHardy's Table 3
    were recovered. Kao itself is paywalled with no OA copy (Unpaywall confirms `is_oa: false`).
  - **Lower trapezius** — no value at any phase, either side, despite Kao instrumenting it separately.
  - **Rhomboid major vs minor**, and **serratus anterior upper vs lower digitations** — not separable.
  - **Latissimus dorsi** — now recovered from the Pink 1990 scan (§2.9), but **single-source**: it never
    enters McHardy's top-two table, so no independent cross-check was possible.
  - **Jobe 1989's per-muscle men-vs-women breakdown** — abstract reports only the non-significant overall
    trend.
  - **Jobe 1986's four segment names and boundaries** — paywalled; the 5-phase scheme postdates it.
- **Flexor carpi radialis, flexor carpi ulnaris, and extensor carpi radialis brevis numeric values from
  Farber et al. 2009** — the study fine-wire-tested all four muscles (including pronator teres), but
  every accessible summary (PubMed abstract, a secondary blog citing the paper) reports pronator teres
  results only. FCR/FCU/ECRB numbers likely exist in the paper's results tables but were not accessible.
- **Pectoralis major head-specific (sternal vs clavicular) data**: not found in any source — every study
  treats it as one muscle.
- **Teres minor, teres major, supinator, intrinsic hand/grip muscles** (interossei, lumbricals, thenar,
  hypothenar): no golf-swing-specific EMG data found — confirmed absent from the accessible literature,
  not merely unsearched. Each was independently searched. **Do not assign these muscles a value.**
  - Nearest supinator proxy is an "extensor–supinator mass" composite electrode in *baseball pitching*
    (van Trigt et al., *Front Sports Act Living* 2021, PMCID PMC8669487), 21–40% of normalised max at
    maximal external rotation, throwing arm. Not golf, composite electrode, not the isolated muscle.
- **Triceps brachii and brachioradialis are NO LONGER in the zero-data category** — corrected in §3.2 and
  §3.3. Trail-arm values exist (triceps long head 50% MVC downswing; brachioradialis 45% MVC backswing;
  Pezarat-Correia 2006, n=3). **Lead-arm values for both remain absent.** This correction supersedes any
  earlier note, including TASKS.md finding F-018, that grouped these two with the zero-data muscles.
- **Flexor digitorum profundus, extensor carpi radialis longus, extensor digitorum**: no per-phase golf
  data. Extensor digitorum was recorded by Verikas et al. 2016 but for onset timing only, no amplitude.
- **Absolute grip-force values in N/kg by precise swing phase**: only approximate, graph-read (Koike
  2005, n = 2) or secondarily-cited (Schmidt 2007 thesis, not independently verified) figures were
  recovered. A precise, primary-source, address-through-impact grip-force curve in absolute units remains
  unverified.
- **Glazebrook et al. 1994's own four-phase scheme**: only “address” and “contact” are named in the
  accessible abstract; the other two phase names/boundaries in their scheme were not recoverable.
- **RESOLVED for subscapularis and pectoralis major — see §1A.** The per-side split is now quantified,
  and it only partly matches the mechanistically plausible reading:
  - **Subscapularis is trail-dominant as expected** — 68% vs 41% at acceleration, and higher trail-side
    in every phase after takeaway.
  - **Pectoralis major is NOT cleanly trail-dominant** — it reads 93% on both sides at acceleration. The
    trail side ramps earlier (64% vs 18% at forward swing), so the asymmetry is in *timing*, not peak
    magnitude. See §1A's flagged anomaly on the identical cross-side values.
  - **Latissimus dorsi remains unquantified per side** — do not assume trail-dominance for it.
- **Sci-hub and similar mirror links surfaced in DuckDuckGo results for at least two of the classic
  papers (Kao 1995, Farber 2009) and were deliberately not used**, per this project's requirement to
  work from legitimate sources only — flagged so a future pass does not mistake their absence here for
  an oversight.
- **The shoulder and scapular data has never been replicated.** Every review from 2004 to 2025 (Kim 2004,
  McHardy & Pollard 2005, Escamilla & Andrews 2009, Marta et al. 2012) re-cites the same Kerlan-Jobe
  fine-wire dataset collected 1986–1995. The forearm *has* been re-measured repeatedly since (Farber
  2009, Sorbie 2016/2017, Robinson 2023, Bochnia 2024, Grieß 2026); the shoulder has not. So every
  shoulder/scapular number in this document traces to **one lab, one cohort era, n=7–15 per study**,
  with no independent confirmation. Weight the app's confidence accordingly: forearm activation is
  multiply-sourced, shoulder activation is single-sourced.
- **There is no Jobe/Perry/Pink elbow paper**, contrary to a reasonable assumption that one exists.
  Confirmed against McHardy & Pollard's reference list: the Kerlan-Jobe golf series covers shoulder,
  scapula, trunk, hip and knee only. The group's forearm paper is Farber et al. 2009, published under the
  Kerlan-Jobe Orthopaedic Clinic name (the successor institution to Centinela Hospital), not under the
  Centinela name.
- **Whether foot-switches were used** to synchronise the golf EMG recordings could not be confirmed —
  foot-switch synchronisation is a hallmark of the same lab's *gait* studies, but the golf papers
  document cinematography (450 fps film) with electronic synchronisation. Do not cite foot-switches for
  the golf work.

---

## Master source list (deduplicated)

1. Jobe FW, Moynes DR, Antonelli DJ (1986). “Rotator Cuff Function During a Golf Swing.” *Am J Sports
   Med* 14(5):388–392. PMID 3777315. DOI 10.1177/036354658601400509.
2. Jobe FW, Perry J, Pink M (1989). “Electromyographic Shoulder Activity in Men and Women Professional
   Golfers.” *Am J Sports Med* 17(6):782–787. PMID 2624291.
3. Pink M, Jobe FW, Perry J (1990). “Electromyographic Analysis of the Shoulder During the Golf Swing.”
   *Am J Sports Med* 18(2):137–140. PMID 2343980. DOI 10.1177/036354659001800205.
4. Kao JT, Pink M, Jobe FW, Perry J (1995). “Electromyographic Analysis of the Scapular Muscles During a
   Golf Swing.” *Am J Sports Med* 23(1):19–23. PMID 7726345. DOI 10.1177/036354659502300104.
5. Glazebrook MA, Curwin S, Islam MN, Kozey J, Stanish WD (1994). “Medial Epicondylitis: An
   Electromyographic Analysis and an Investigation of Intervention Strategies.” *Am J Sports Med*
   22(5):674–679. PMID 7810792. DOI 10.1177/036354659402200516.
6. Farber AJ, Smith JS, Kvitne RS, Mohr KJ, Shin SS (2009). “Electromyographic Analysis of Forearm
   Muscles in Professional and Amateur Golfers.” *Am J Sports Med* 37(2):396–401. PMID 19022991.
7. Bochnia JM, Bockholt S, Gosheger G, Theil C, Schneider KN (2024). “An Ergonomic Golf Grip Leads to
   Lower Forearm Muscle Activity — A Prospective Case Series of 30 Right-Handed Amateur and Professional
   Golfers.” *BMC Musculoskelet Disord* 25(1):668. PMID 39187838. PMC11346012.
8. Grieß D, Schneider KN, Gosheger G, Theil C, Bochnia JM, Bockholt S (2026). “Graphite Shafts Reduce
   Forearm Muscle Activity in Golf — A Prospective Case Series of 40 Right-Handed Amateur and
   Professional Golfers.” *BMC Musculoskelet Disord*. PMC12930853.
9. Robinson PG, Carson HJ, Richards J, Murray A, Duckworth AD, Campbell D (2023). “What Differences
   Exist Between the Lead and Trail Wrist in Extensor Carpi Ulnaris Activity and Golf Swing Joint
   Kinematics in Sub-Elite Golfers?” *J Sports Sci* 41(17):1596–1604. PMID 37983261.
10. Marta S, Silva L, Castro MA, Pezarat-Correia P, Cabri J (2012). “Electromyography Variables During
    the Golf Swing: A Literature Review.” *J Electromyogr Kinesiol* 22(6):803–813. PMID 22542769.
11. McHardy A, Pollard H, Luo K (2006). “Golf Injuries: A Review of the Literature.” *Sports Med*
    36(2):171–187. PMID 16464124.
12. Escamilla RF, Andrews JR (2009). “Shoulder Muscle Recruitment Patterns and Related Biomechanics
    During Upper Extremity Sports.” *Sports Med* 39(7):569–590. PMID 19530752. (Review; golf-specific
    %MVIC figures are secondary aggregates within a multi-sport review, not this document's own primary
    measurement — treat accordingly.)
13. Langlais SM, Broker JP (2014). “Grip Pressure Distributions and Associated Variability in Golf: A
    Two-Club Comparison.” *Sports Biomech* 13(2):109–122. PMID 25122996.
14. Koike S, Shiraki H, Fujii N, Ae M (2005). “Kinetic Analysis of Each Hand During Golf Swing with Use
    of an Instrumented Golf Club.” *Proceedings of the ISB XXth Congress / ASB 29th Annual Meeting*,
    Cleveland, OH, p. 515. (Directly read, primary conference-proceedings PDF; n = 2 professional
    golfers — small-sample caveat applies throughout §6.)
15. Schmidt ER (2007). PhD thesis, Loughborough University. “Measurement of Grip Force and Evaluation of
    Its Role in a Golf Shot.” **Accessed only via secondary citation (tutelman.com); primary thesis not
    independently verified this session — lower confidence, flagged throughout §6.**
16. Verikas A, Vaiciukynas E, Gelzinis A, Parker J, Olsson MC (2016). “Electromyographic Patterns During
    Golf Swing: Activation Sequence Profiling and Prediction of Shot Effectiveness.” *Sensors (Basel)*
    16(4):592. PMC4851105. (8-channel sEMG incl. bilateral FCR, EDC, rhomboideus, trapezius; used for
    onset-timing/sequencing insight in §4 cross-reference — no amplitude values reported by the paper
    itself, it is a classification/timing study.)
17. Tutelman T. “Required Grip Pressure.” tutelman.com/golf/swing/gripPressure.php — secondary/
    enthusiast source, used only as a pointer to Schmidt (2007) and Koike et al.; its own physics-based
    calculated grip-force-vs-clubhead-speed estimates (e.g. “100 mph → 92 lb”) are **the site author's own
    calculations, not empirical measurements, and are not reproduced in this document as findings.**

### Added on the second research pass

18. McHardy A, Pollard H (2005). “Muscle Activity During the Golf Swing.” *Br J Sports Med*
    39(11):799–804. PMID 16244187. PMCID PMC1725059. **Source of the scapular %MMT figures in §1A via
    its Table 3**, which lists the two most active muscles per side per phase from Pink 1990 and
    Kao 1995. Distinct from McHardy, Pollard & Luo 2006 (item 11), which is the injury review.
19. Pink M, Jobe FW, Perry J (1990). “Electromyographic Analysis of the Shoulder During the Golf Swing.”
    *Am J Sports Med* 18(2):137–140. PMID 2343980. Full %MMT grid in §1A recovered from a scanned copy
    and cross-validated 9/9 against item 18's Table 3.
20. Pezarat-Correia P, Cabri J, Fernandes O, Sousa JP (2006). “Electromyographic Analysis of the Dominant
    Upper Limb During the Golf Swing.” *Proc ECSS Lausanne* 3(1):70–85. ISSN 19360533. Sole golf source
    for trail-arm triceps brachii (50% MVC) and brachioradialis (45% MVC); also biceps (26%) and
    latissimus dorsi (53%). **n=3, trail arm only, 3-phase scheme, conference proceedings — indicative
    only.**
21. Sorbie GG, Hunter HH, Grace FM, Gu Y, Baker JS, Ugbolue UC (2016). “An Electromyographic Study of the
    Effect of Hand Grip Sizes on Forearm Muscle Activity and Golf Performance.” *Res Sports Med*.
    PMID 27267082. Second independent skill-level forearm finding (§9).
22. Sorbie GG, Darroch P, Grace FM, Gu Y, Baker JS, Ugbolue UC (2017). “Commercial Golf Glove Effects on
    Golf Performance and Forearm Muscle Activity.” *Res Sports Med*. PMID 28819996.
23. Choi H, Park S (2020). “Three Dimensional Upper Limb Joint Kinetics of a Golf Swing with Measured
    Internal Grip Force.” *Sensors* 20(13):3672. PMID 32630024. PMC7374515. Source of the trail-hand
    threefold-torque and lead-precedes-trail 50–200 ms timing findings (§6).
24. Budney DR (1979). “Measuring Grip Pressure During the Golf Swing.” *Res Q* 50(2):272–277.
    PMID 472468. **No abstract on PubMed, no accessible full text — cited for completeness, contributes
    no usable data.**
25. Pink M, Perry J, Jobe FW (1993). “Electromyographic Analysis of the Trunk in Golfers.” *Am J Sports
    Med* 21(3):385–388. PMID 8346752. Source of the verbatim 5-phase boundary definitions and of the
    binary 30%-MMT banding noted in §8.
26. van Trigt B, Galjee E, Hoozemans MJM, van der Helm FCT, Veeger DHEJ (2021). “Establishing the Role of
    Elbow Muscles by Evaluating Muscle Activation and Co-contraction Levels at Maximal External Rotation
    in Fastball Pitching.” *Front Sports Act Living*. PMC8669487. **Baseball, not golf** — used only as
    the flagged supinator proxy in §10.
27. Nakamura G, Abe M, Kumano H (2019). “Acute Compartment Syndrome of the Forearm Secondary to Hematoma
    after Playing Golf.” *J Hand Surg Asian Pac Vol*. Clinical case report, lead-arm brachioradialis;
    not activation data (§3.3).
28. Kim DH, Millett PJ, Warner JJP, Jobe FW (2004). “Shoulder Injuries in Golf.” *Am J Sports Med*
    32(5):1324–1330. Injury-laterality context (>90% of golfers' shoulder problems involve the lead
    shoulder; lead-shoulder injuries ~3× trail).

## Cross-reference

- [[T-011a-phase-taxonomy-and-timing]] — swing-phase model and timing this document's phase mapping (§1)
  depends on.
- [[07-verbatim-source-tables]] — verbatim McHardy & Pollard 2005 Tables 3 and 4, Kim et al. 2004 Table 2
  (the only complete both-sides all-phases scapular grid, ordinal), and the Pink 1990 latissimus dorsi
  row. Independently confirms this document's §1A extraction cell-for-cell, including the identical
  93/93 and 74/74 pectoralis major values flagged there. **Read its "blank cells are not zero" warning
  before using any Table 3 figure.**
