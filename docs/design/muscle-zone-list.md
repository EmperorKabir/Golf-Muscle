# Muscle zone list (T-012)

The definitive list of muscle zones the model renders. Every zone is drawn **twice** — lead and trail side,
independently coloured — because lead/trail asymmetry is the defining feature of the golf swing. 57 groups ×
2 sides = **114 independently rendered zones**.

## Governing principles

1. **Err toward more groups** (user instruction, D-002 context). Unused muscles are useful contrast.
2. **Split where the literature splits.** Upper/middle/lower trapezius, upper/lower serratus, thoracic/lumbar
   erector spinae and upper/lower gluteus maximus are all split because published sources report them
   separately. Pectoralis major is **not** split into sternal and clavicular heads, because no golf source
   ever does (F-018) — splitting it would invent a distinction the data cannot support.
3. **Include muscles that have never been measured.** They are anatomically real and their absence would be a
   silent lie about the body. They render in the unmeasured state (F-009, F-013, F-018).
4. **Never render an unmeasured muscle as inactive.** See the data-confidence tiers below.

## Data confidence tiers — these drive the render state

| Tier | Meaning | Render treatment |
|---|---|---|
| **A** | Numeric per-phase values obtained from an accessible source | Full colour, normal confidence |
| **B** | Measured in a golf study, but magnitude inaccessible (paywalled or unretrieved). Timing pattern known | Colour with a visible uncertainty treatment |
| **C** | Measured in a golf study but amplitude never reported by the authors | Uncertainty treatment, wider band |
| **D** | **Never measured in golf.** No data exists anywhere | **Unmeasured state — outline only, explicitly marked. Never transparent-as-zero** |

Tier D is not a failure of our research. For eight of these, exhaustive searching confirmed the gap, and for
iliopsoas the absence is stated in print by Marta et al. 2012.

## Shoulder girdle and scapula

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 1 | Upper trapezius | A | 52% MMT trail, backswing — the most active upper-body muscle of that phase |
| 2 | Middle trapezius | A | 51% MMT lead forward swing; 37% MMT trail backswing |
| 3 | Lower trapezius | B | Measured by Kao 1995; no value in any accessible table (F-020) |
| 4 | Rhomboids | A | 68% MMT lead forward swing — highest lead-side upper-body value; full Kim grid |
| 5 | Levator scapulae | A | 62% MMT lead acceleration; full Kim grid |
| 6 | Serratus anterior, upper | A | 58% MMT trail forward swing; 69% MMT trail acceleration |
| 7 | Serratus anterior, lower | A | 40% MMT trail late follow-through (reported combined with upper) |

Distinctive pattern worth surfacing in the UI: **lead-side serratus anterior shows constant low activity
across the entire swing** (Kim et al. 2004), which is the mechanism behind a real fatigue complaint in
golfers. It is the only muscle in the body with a flat profile.

## Rotator cuff

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 8 | Supraspinatus | A | Full Pink 1990 grid. Trail 25/14/12/7/7 (peaks back swing); lead 21/21/18/28/28 (peaks follow-through) |
| 9 | Infraspinatus | A | Trail 27/13/7/12/9; lead 14/16/27/**61**/40. Sharpest side-inversion in the body |
| 10 | Subscapularis | A | Trail 16/49/**68**/64/56; lead 33/29/41/23/35. Trail-dominant throughout |
| 11 | Teres minor | D | **Never measured in golf** (F-018) |

## Shoulder and upper arm

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 12 | Pectoralis major | A | Trail 12/64/**93**/74/37; lead 21/18/**93**/74/39. Identical peak both sides — trail concentric, lead eccentric. Not split into heads (F-018) |
| 13 | Latissimus dorsi | A | Trail 9/**50**/47/39/28; lead 17/**46**/31/32/18. Peak phase disputed three ways (F-024) |
| 14 | Anterior deltoid | A | Trail 5/**21**/10/11/8; lead 13/9/10/21/**26**. Side-inverted, low throughout |
| 15 | Middle deltoid | A | 2–8% across all phases, **no pattern — quantitatively non-contributory** |
| 16 | Posterior deltoid | A | 5–24% across all phases, **no pattern — quantitatively non-contributory** |
| 17 | Teres major | D | **Never measured in golf** (F-018) |
| 18 | Biceps brachii | B | Peak phase disputed: backswing (26% MVC, n=3) vs late follow-through (raw µV, n=30/40). Unresolved (F-028) |
| 19 | Triceps brachii, trail | B | 50% MVC peaking downswing (Pezarat-Correia 2006, n=3, conference proceedings — indicative only) |
| 19b | Triceps brachii, lead | D | **Never measured** — trail-only data exists |

## Forearm and hand

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 20 | Wrist and finger flexors | A | **90.77% MVC burst at contact** (Glazebrook 1994) — highest true-%MVC figure in the upper limb (F-017). The "flexor burst", attributed to the trail side |
| 21 | Wrist and finger extensors | A | 33.59% MVC at address ramping to 58.77% MVC at contact (Glazebrook 1994) |
| 22 | Pronator teres | A | Farber 2009 %MMT: amateur trail 120.9% vs professional 57.4% — the clearest skill contrast found anywhere (F-019) |
| 23 | Brachioradialis, trail | B | 45% MVC peaking backswing (Pezarat-Correia 2006, n=3) — highest elbow-flexor value in the golf literature |
| 23b | Brachioradialis, lead | D | **Never measured.** Only a clinical case report of lead-forearm compartment syndrome establishes loading |
| 24 | Supinator | D | **Never measured in golf** (F-018) |
| 25 | Intrinsic hand and grip muscles | D | **Never measured in golf** (F-018). Grip *force* data exists but is not EMG, and varies ~3× by sensor method |

## Trunk, anterior

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 26 | Rectus abdominis, upper | B | Measured bilaterally by Watkins 1996; table paywalled |
| 27 | Rectus abdominis, lower | B | As above |
| 28 | External oblique | A | 59–67% EMGmax trail (Marta 2013); 59% MMT trail acceleration (McHardy) |
| 29 | Internal oblique | C | Measured by Horton 2001 but **amplitude never reported**. Only recoverable number is a trivial +1% MVC club difference |
| 30 | Transversus abdominis | D | **Never measured in golf** — confirmed by three independent research passes |

## Trunk, posterior

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 31 | Erector spinae, thoracic | A | Li 2023 full five-phase bilateral T8 table. Lead peaks at **early follow-through** (51.8%), a phase later than the classic narrative |
| 32 | Erector spinae, lumbar | A | Li 2023 L3 table (13–52% MVC). **Magnitude disputed 2–3× against Sorbie 2018 (67–106% MVC)** — F-011. Carry both |
| 33 | Multifidus | D | **Never measured in golf** — confirmed by three independent passes |
| 34 | Quadratus lumborum | D | **Never measured in golf**. One paper *estimates* it via a model using other muscles as input |

## Hip and pelvis

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 35 | Gluteus maximus, upper | A | **100% MMT trail, forward swing** — the highest single value in the entire dataset (F-022) |
| 36 | Gluteus maximus, lower | A | **98% MMT trail, forward swing.** Corroborated independently at 62–72% EMGmax (Marta 2013) |
| 37 | Gluteus medius | A | 51% MMT trail acceleration; 59% MMT trail early FT |
| 38 | Gluteus minimus | D | **Never measured in golf.** Too deep for surface EMG; no fine-wire golf study exists |
| 39 | Deep hip external rotators | D | **Never measured in golf** (piriformis, obturators, gemelli, quadratus femoris) |
| 40 | Tensor fasciae latae | D | **Never measured in golf.** Appears in the literature only as a confound to be excluded |
| 41 | Iliopsoas | D | **Never measured in golf — gap explicitly stated in print** by Marta et al. 2012 |
| 42 | Adductor magnus | A | 63% MMT lead forward swing; 35% MMT lead late FT. Initiates pelvic rotation with the trail hip extensors |
| 43 | Adductor longus and brevis | D | **Never separated from adductor magnus** in any golf source |

## Thigh

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 44 | Rectus femoris | B | Measured by Marta 2016; significant club effect confirmed, magnitude unretrieved |
| 45 | Vastus lateralis | A | **88% MMT lead forward swing**; 58% acceleration; 59% early FT; 40–42% late FT |
| 46 | Vastus medialis | B | Measured by Marta 2016; club effect confirmed, magnitude unretrieved |
| 47 | Vastus intermedius | D | **Never measured in golf** — lies deep to rectus femoris |
| 48 | Biceps femoris (long head) | A | 78% MMT trail forward swing; 83% MMT lead acceleration; 79% lead early FT. Also 68–73% EMGmax trail |
| 49 | Semitendinosus | A | **70–76% EMGmax trail forward swing** — highest lower-limb value in Marta 2016 |
| 50 | Semimembranosus | A | 28% MMT trail backswing; 42% MMT lead late FT |

## Lower leg

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 51 | Gastrocnemius, medial head | B | Measured by Marta 2016; club effect confirmed, magnitude unretrieved |
| 52 | Gastrocnemius, lateral head | B | As above |
| 53 | Soleus | D | **Never isolated from gastrocnemius** in any golf study |
| 54 | Tibialis anterior | B | Measured by Marta 2016; significant club effect, magnitude unretrieved |
| 55 | Peroneus longus | B | Measured by Marta 2016; significant club effect, magnitude unretrieved |

## Neck

| # | Zone | Tier | Evidence |
|---|---|---|---|
| 56 | Sternocleidomastoid | D | Barclay & McIlroy 1990 studied neck muscles, but no finding of theirs is reproduced in any accessible source |
| 57 | Cervical extensors (splenius, semispinalis) | D | **Never measured in golf** |

## Summary by tier

Revised after the full Pink 1990 shoulder grid became available (2026-08-04). Seven zones moved up a tier;
two split into a measured trail side and an unmeasured lead side. 59 zone entries.

| Tier | Count | Share |
|---|---|---|
| A — numeric data available | 30 | 51% |
| B — measured, magnitude inaccessible or weak-sample | 10 | 17% |
| C — measured, never reported | 1 | 2% |
| D — never measured in golf | 18 | 30% |

**Roughly a third of the human musculature relevant to the golf swing has never been measured during one.**
That is the single most important fact this research produced, and the model must state it rather than hide
it behind a transparent zone.

### Two findings that are content, not gaps

**Middle and posterior deltoid do almost nothing.** 2–8% and 5–24% respectively, no pattern across phases.
Jobe 1986 states the deltoid is inactive on the trail side throughout, and on the lead side "except for a
brief spurt from the anterior portion during the milliseconds immediately preceding ball contact." Two large,
visually prominent shoulder muscles that stay cold through the whole swing — exactly the contrast the user
asked to preserve.

**Lead serratus anterior is the only flat muscle in the body.** Constant low activity across the entire
swing rather than phasic. Offered by Kao 1995 as the fatigue mechanism in high-volume golfers.

### Confidence is not uniform across the body

Shoulder and scapular data is **single-lab, single-era, never replicated** — Kerlan-Jobe, 1986–1995, n=7–15
per study. The forearm has **five independent modern replications** (Farber 2009, Sorbie 2016/2017, Robinson
2023, Bochnia 2024, Grieß 2026). A tier-A shoulder value and a tier-A forearm value do not carry equal
weight, and the renderer's uncertainty treatment should reflect that.

## Consequences for the renderer

1. **Four render states, not two.** Active, inactive, uncertain (tiers B and C), and unmeasured (tier D).
   Study 09's reveal rule from the style studies applies only to tier A and B zones.
2. **Zone outlines are always drawn.** Only fill is conditional. This preserves the contrast requirement and
   keeps tier D zones honestly visible.
3. **Units cannot be pooled.** Tier A splits across %MMT, %MVC, %EMGmax and raw µV (F-010, F-016). The
   activation model needs either a documented conversion or per-unit segregation before any value reaches the
   colour ramp. **This is the blocking task for T-021.**
4. **Two muscles anchor the top of the scale**: trail gluteus maximus (100%/98% MMT, corroborated at 62–72%
   EMGmax) and bilateral pectoralis major (93% MMT). Wrist flexors at 90.77% MVC anchor the upper limb.
5. **Posterior view is essential, not optional.** The two highest-activation muscles in the body — gluteus
   maximus and the hamstrings — are invisible from the front. The current style studies show only anterior
   zones and therefore omit the most important part of the swing.

## Open items this list creates

- T-019: define the unit-reconciliation strategy across %MMT / %MVC / %EMGmax / raw µV before T-021.
- T-020 (new sub-item): design the visual language for the four render states.
- Posterior-view geometry must be authored before the model can claim to meet the all-angles requirement.
