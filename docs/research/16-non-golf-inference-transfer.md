# 16 — Non-Golf Inference Transfer: Validating and Operationalising the Analogue-Transfer Strategy

Status: IN PROGRESS (incremental write, single WebFetch-only session, no sub-agents per operating constraints)

## Purpose

Validates the project owner's claim: muscle usage for the ~66% of muscle-zones with no golf EMG data can be inferred by researching the same muscles performing their generic or task-shared function outside golf (e.g. diaphragm/core during forced breathing, deep hip rotators during pivoting in other sports), always with a golf-first source preference. This document (1) tests whether that strategy is scientifically defensible, (2) builds a graded transfer-validity rulebook, (3) harvests actual %MVC-style data for golf-unmeasured muscles from non-golf sources, (4) surveys rotational-sport EMG (the closest analogue tier), and (5) states which muscles remain unfillable even with transfer.

---

## 1. Is EMG transfer across tasks scientifically defensible? Literature on task-specificity

**Answer: conditionally yes, but only under a stated, testable set of matching conditions — never as a default assumption.** The literature converges on a specific framework (below) rather than a binary "transfer works / doesn't work" verdict; the owner's instinct is directionally correct but currently unbounded, and this section supplies the bounds.

### 1.1 The governing framework: Dynamic Correspondence (Verkhoshansky)

The most directly applicable existing framework is **"dynamic correspondence" (DC)**, created by Yuri Verkhoshansky in the early 1990s and formalised in strength-and-conditioning science (Source 1: PMID 36412764 / PMCID PMC9680266, *J Funct Morphol Kinesiol* 2022, open access narrative review). DC states that a training stimulus (or, by direct extension, an EMG/activation measurement) transfers to a target task **only to the degree that both share each of the following variables**:

1. **Amplitude and direction of movement** — range of motion and movement vector must match; the review notes force in sport is often applied through the ground, so closed-chain analogues transfer better than open-chain ones.
2. **Accentuated region of force production** — *where in the range of motion* peak force/activation occurs must correspond, not just the total range.
3. **Dynamics of effort** — the force-velocity profile (how force and speed trade off through the movement) must align.
4. **Rate and timing of maximum force production** — matching the sport's actual time-to-peak-force window (e.g. fast vs slow stretch-shortening cycle) is required; a mismatch invalidates transfer even if peak magnitude matches.
5. **Regime of muscular work** — contraction mode (concentric / eccentric / isometric / stretch-shortening cycle) must match; the review states plainly that "different adaptations take place between concentric and eccentric actions."
6. **Segmental interrelation** (added by Goodwin & Cleather, cited in the same review) — the joint-to-joint coordination pattern (which segments move together and in what order) must correspond, not just the prime-mover muscle.

The review explicitly documents **transfer failure modes**: open kinetic chain exercises "are not likely to transfer to the same degree even if the muscle groups used are similar"; elastic-band resistance increases strength/power metrics but shows "little evidence" of transfer to jump performance because it alters the force-production region; and even DC-compliant exercises fail to transfer if improperly sequenced in training. This gives a positive framework (what must match) and confirms that similarity of *prime mover muscle alone is insufficient* — a recurring risk in the owner's proposed strategy that must be guarded against explicitly.

### 1.2 EMG-specific evidence of non-transfer between contraction modes

Independent of the DC framework, direct EMG studies confirm that **the EMG-to-force relationship itself is not constant across contraction mode**, which is the more granular mechanism underlying DC criterion 5:

- Source 2 (Ruas et al., PMID 39367883, *Eur J Appl Physiol* 2025): during maximal knee extension, EMG-to-torque ratio was **lower for eccentric than for isometric and concentric** contractions — the same %MVC EMG signal corresponds to a different force depending on contraction mode.
- Source 3 (Desachy et al., PMID 40547839, *Front Aging Neurosci* 2025): "muscular activity was lower during eccentric than concentric contractions" at matched output.
- Source 4 (Haigney et al., PMID 40755446, *Eur J Neurosci* 2025): at low intensity (25% MVC) no significant excitability difference was found across isometric/concentric/eccentric actions — i.e. the divergence is itself load- and intensity-dependent, not a fixed offset, which rules out using a simple correction factor.

This directly corroborates the project's own existing finding (F-037, `12-functional-anatomy-and-moment-arms.md`): eccentric contraction can produce the *same or lower* EMG amplitude than concentric while performing the opposite mechanical role — already documented in golf for lead/trail pectoralis major (McHardy & Pollard 2005) and gluteus medius (Edwards et al. 2020). The new sources generalise this beyond golf, confirming it is a general neuromuscular property, not a golf-specific artefact — which strengthens (not weakens) the case that any transferred %MVC figure must be tagged with its source contraction mode and never silently equated with a different mode.

### 1.3 Velocity specificity

- Source 5 (meta-analysis, PMID 40839186, *Sports Med Open* 2025): eccentric-only isokinetic training improves eccentric MVC more than concentric or isometric MVC; **training/measuring at one velocity does not equally transfer to another**, and the effect shrinks further when training velocity and testing velocity diverge.
- Source 6 (PMID 40363107, *Sensors* 2025): the optimal EMG normalisation method itself varies by task and muscle, meaning cross-task EMG comparison additionally carries a *methodological* (not just physiological) transfer risk — pooling EMG data normalised differently across source studies (already flagged in this project as F-010/F-016) compounds the transfer problem when the sources being pooled are non-golf.

No source located gives a quantitative "decay function" for transfer as velocity mismatch increases; all evidence found is qualitative (transfer degrades, direction and rough magnitude confirmed, no interpolatable curve). This is stated as a limit, not filled by extrapolation.

### 1.4 Task-dependent recruitment within the *same* muscle

A further, more severe caveat: several 2025–2026 motor-unit studies show that **recruitment can differ regionally within one muscle depending on task, even at matched net joint torque** — meaning "same muscle, same force" is not by itself sufficient for transfer:

- Source 7 (PMID 42031565, *J Neurosci* 2026): 9/10 participants could voluntarily dissociate vastus medialis from vastus lateralis motor-unit activity; selective recruitment was possible specifically in proximal VM, not distal VM/VL — compartmentalised, task-dependent control within a single named "muscle."
- Source 8 (PMID 42287257, *Scand J Med Sci Sports* 2026): hamstring motor-unit discharge differed between hip-extension-dominant and knee-flexion-dominant tasks at matched force, with region-dependent (proximal vs distal) variability.
- Source 9 (PMID 41615326, *J Appl Physiol* 2026): soleus/medial/lateral gastrocnemius show independent directional tuning in single-leg stance that collapses to uniform activation in double-leg stance — the same triceps surae "muscle group" is task-fractionated.

**Consequence for the transfer rulebook:** even Tier 1 transfer (same muscle, near-identical task) should be read as applying to the muscle as a *named EMG electrode site*, not as a guarantee that every motor-unit pool/compartment within it behaves identically; this is a known residual uncertainty, not resolved by any source found.

### 1.5 Verdict on the owner's claim

The claim is **scientifically defensible as a research strategy, not as an assumption**. It is defensible because: (a) a peer-reviewed, decades-old framework (DC) exists specifically to define when cross-task transfer is valid, giving a non-arbitrary test rather than ad hoc judgement; (b) EMG/motor-control literature independently corroborates that mismatches in contraction mode, velocity, and even within-muscle region measurably break transfer, which means the framework's warnings are empirically grounded, not merely theoretical. It stops being defensible the moment a source is transferred without checking it against the DC criteria and without labelling the resulting record's confidence accordingly — i.e. "diaphragm is active in forced breathing, therefore diaphragm activity during the swing is X%" is illegitimate; "diaphragm shows feedforward pre-activation ahead of prime-mover onset in loaded postural tasks, and this feedforward architecture is shown to generalise across at least four different loaded/rotational tasks, therefore feedforward pre-activation timing (not magnitude) can be inferred for the swing, at reduced confidence" is legitimate. Section 2 formalises this into a graded rulebook.

---

## 2. The Transfer Rulebook

Built from the Dynamic Correspondence criteria (§1.1) applied specifically to muscle-activation (not training-adaptation) transfer, cross-referenced against this project's existing evidence-boundary finding (F-046: pressure/force data proves force passed through a region but cannot yield a named muscle's %MVC) and permanence finding (F-049: some muscles are unmeasurable by any method compatible with a full-speed swing). Every harvested record in §3–4 is tagged with its tier.

### Tier 1 — Same muscle, near-identical task (rotational/ballistic striking-throwing sports)
**Matches:** contraction regime (fast SSC), rate of force development, whole-body proximal-to-distal sequencing, axial-rotation dominance, ballistic single-effort structure. **Differs:** external implement, exact joint angles, sport-specific technique variance between athletes.
**Can justify:** approximate peak %MVC magnitude (with wide band), relative activation *ranking* across muscles in the kinetic chain, and phase-relative timing (e.g. "trunk rotators peak before shoulder rotators peak" ordering). **Cannot justify:** a precise numeric %MVC value transplanted as if golf-measured; exact timing in absolute milliseconds (golf's own swing duration and phase proportions differ from pitching/serving); direction-specific claims where anatomy of the analogue task differs (e.g. a two-handed bat swing vs one-handed golf grip changes forearm loading pattern).

### Tier 2 — Same muscle, shared mechanical demand, different task (weight-shift, single-leg stance, loaded trunk rotation, pivoting/cutting)
**Matches:** the specific mechanical *demand* class only (e.g. frontal-plane hip stabilisation during single-leg loading, or axial trunk stabilisation under rotational torque) — not the whole movement.
**Can justify:** *that* the muscle is active and *roughly which phase-type* recruits it (e.g. "active during weight transfer," "active during deceleration/stabilisation") — a presence/absence and coarse-phase claim only. **Cannot justify:** any specific %MVC magnitude carried over numerically, any fine-grained timing, or contraction-mode assumptions (per §1.2, a muscle stabilising eccentrically in a cutting task may show different EMG amplitude than the same muscle stabilising concentrically in golf's analogous phase).

### Tier 3 — Same muscle, generic function only (quiet standing, resting breathing, isolated joint-motion testing)
**Matches:** anatomical action and innervation only.
**Can justify:** *that the muscle exists and is capable of the mechanical role anatomy predicts* (mechanical necessity/anatomical obligation — the two legitimate inference routes already defined in T-048) — e.g. "the diaphragm participates in postural stabilisation feedforward of prime-mover onset in loaded tasks generally, therefore it plausibly does so in the golf swing too." **Cannot justify:** any numeric activation value, timing value, or amplitude at all. This is the tier golf-unmeasured muscles mostly fall into (§3), and it is the tier F-046's foot-muscle boundary describes: proof that force/demand exists, never a specific muscle's %MVC.

### Tier 0 (new, added by this document) — Mechanical/force evidence without EMG at all
Not EMG transfer but adjacent: GRF, pressure, torque, ultrasound-thickness or IAP data proving a mechanical demand exists in golf itself, without any muscle-level attribution. This is the existing F-046/F-048 category. Combining Tier 0 golf-specific mechanical proof with Tier 3 non-golf generic-function EMG is the *strongest available combination* for the permanently-unmeasurable muscles (§3.1) — it is still not measurement, but it is the most constrained inference route available, and should be labelled explicitly as "Tier 0+3 combined inference," never upgraded to look like a Tier 1 or 2 record.

### Rulebook usage rule
Every non-golf record entering the dataset schema (T-042) must carry: source task, tier (0/1/2/3), which DC criteria matched vs mismatched, and the specific claim type permitted (magnitude / ranking / phase-presence / existence-only). A record that cannot state which DC criteria matched does not get a tier — it is excluded, not defaulted to Tier 3, because Tier 3 itself requires the anatomical-action match to be explicit, not assumed.

---

## 3. Harvested non-golf data for golf-unmeasured muscles

(writing in progress)

---

## 4. Rotational-sport EMG (closest analogue tier)

(writing in progress)

---

## 5. Limits — what remains unfillable

(writing in progress)

---

## Source log

(populated incrementally; numbered, with PMID/PMCID/URL and one-line takeaway)
