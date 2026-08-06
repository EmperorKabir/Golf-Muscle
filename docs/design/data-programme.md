# The data programme — staged plan

The objective: build a defensible, time-resolved, whole-body picture of muscle activation through the golf
swing, from many partial and incompatible sources, without guessing.

## The method, stated precisely

`09-inverse-activation-estimation.md` established that activation **cannot** be recovered from observed
motion alone. That is a statement about an *under-determined* problem: one observation (the motion), many
unknowns (the muscles), infinitely many solutions.

This programme is the opposite shape. It is **over-determined triangulation**:

- Each measured muscle, in each study, at each phase, is an independent **constraint**.
- The kinematic chain links constraints **across time** — the proximal-to-distal sequence means a muscle
  acting at one joint has consequences for what must be happening at the next joint, at a known later
  instant.
- Functional anatomy links constraints **across the body** — a muscle's origin, insertion and moment arm
  determine what motion it can produce, and the observed joint motion determines whether it was shortening
  or lengthening.
- Multiple independent studies of the same muscle **overlap**, and where they disagree the disagreement is
  itself information.

The result is not a unique solution derived from first principles. It is a **bounded, evidence-anchored
reconstruction whose residual uncertainty is explicitly quantified**. That is achievable and honest.
The distinction from the impossible version is that we are not asking the mathematics to invent information —
we are assembling information that already exists and forcing it to be mutually consistent.

**Stage 7 exists to test whether this actually works**, rather than to assume it does.

## Current position

- 14 research documents, ~460 KB of cited evidence.
- ~120 muscle groups defined; ~30% have numeric data, ~66% have none.
- Five distinct error classes identified that block naive pooling: incompatible units (F-010), raw-µV
  sources (F-016), phase-label ambiguity (F-008/F-023), electrode-type pooling (F-026), and anatomical
  crosstalk (F-039).
- **All of it is prose.** None of it is computable. That is the immediate bottleneck.

## Stage 0 — Schema. Cut every jigsaw piece to the same edge

*Nothing else can proceed until this exists. Prose cannot be cross-referenced.*

Define one record structure that every observation in every document is transcribed into:

| Field | Purpose |
|---|---|
| `muscle_id` | Canonical id from the zone list; pooled sites get an explicit pooled id |
| `side` | lead / trail / midline / unspecified |
| `phase_label` | The source's own label, verbatim |
| `phase_definition` | The source's own printed definition of that label — never inferred (F-008/F-023) |
| `t_start_ms`, `t_end_ms` | Registered to the master timeline in Stage 2 |
| `value`, `unit` | %MMT, %MVC, %EMGmax, raw µV, ordinal — never silently converted |
| `normalisation_ref` | How 100% was defined in that study |
| `electrode_type` | surface / fine-wire / indwelling / ultrasound proxy / model estimate |
| `crosstalk_risk` | Per F-039; high for surface obliques, supraspinatus, subscapularis |
| `n`, `population` | Sample size, skill level, sex, club |
| `contraction_mode` | Assigned in Stage 4, not by the source |
| `confidence_tier` | A/B/C/D per the zone list |
| `source_id`, `verbatim_quote` | Traceability back to the printed figure |

Rule: **a record is never created without a source and a verbatim anchor.** Inferred records are permitted
only in Stage 6 and carry `inference: true` plus their derivation.

## Stage 1 — Unit reconciliation

Blocking task T-019. Resolve the five error classes:

- Decide, with justification, whether %MMT and %MVC can be related at all, or must stay segregated.
- Raw µV is usable only as within-study shape — encode that as a hard constraint, never a magnitude.
- Ordinal (+ to +++++) maps to a band, not a point value.
- Record crosstalk-contaminated values with widened uncertainty rather than discarding them.

Output: either a documented conversion with stated error, or an explicit segregation policy. **Not a fudge
factor.**

## Stage 2 — Timeline registration

Every source uses a different phase scheme — 5-phase Centinela, 4-phase Glazebrook with a real address
sample, Kim's split takeaway, percentage-of-swing, absolute ms.

- Build one master timeline in **real milliseconds** (F-014 route: real time, not percentage).
- Register every source's phases onto it using its own printed boundary definitions.
- Where a source's boundary is ambiguous, record the ambiguity as a time range, not a point.
- Address, top and impact are boundary *instants* that were never sampled (F-014) — mark them as
  interpolated regions, permanently.

## Stage 3 — Per-muscle envelope construction

For each muscle, assemble all its records into a continuous curve using the monotone, mean-preserving
interpolation from `06-activation-curve-and-colour-method.md`:

- Curve plus **uncertainty band**, not a single line.
- Band widens where sources disagree (erector spinae, F-011), where crosstalk is likely (obliques, F-039),
  where only one lab has ever measured it (shoulder, F-031), and across interpolated instants.
- Explicit onset/offset/peak markers with their own uncertainty.

## Stage 4 — Kinematic chain constraint propagation

**This is the core of the user's method and the stage that generates new knowledge.**

For each muscle at each instant, cross-check its activation envelope against:

1. **Joint motion** at that instant (from Stage 2 kinematics): is the joint moving in the muscle's direction
   of action, against it, or not at all? This assigns `contraction_mode` — concentric, eccentric, isometric.
   It is *derived*, not assumed, and it resolves cases like the identical 93%/93% pectoralis reading (F-028).
2. **Moment arm** at that joint angle — noting that moment arms reverse with angle (hip rotators switch from
   external to internal rotators as flexion increases), so a muscle's action is not fixed.
3. **Sequence timing** — the proximal-to-distal chain means a muscle's action at one joint predicts a
   consequence at the next joint after a known delay. A muscle whose activation is inconsistent with the
   downstream motion is either mis-registered in time or mis-attributed.

Each check either **corroborates** a record, **reassigns** it (usually concentric → eccentric), or **flags a
contradiction** for Stage 5.

Known limits to encode honestly: biarticular muscles are ambiguous by Lombard's paradox — a two-joint muscle
can extend a joint it anatomically flexes, given a co-contracting antagonist. Those muscles carry a permanent
ambiguity flag rather than a forced answer.

## Stage 5 — Contradiction audit

Over-determination pays off here. Where two independent constraints disagree about the same muscle at the
same instant, one of these is true:

- A unit or normalisation error (Stage 1 failure).
- A phase mis-registration (Stage 2 failure) — the most likely cause, given F-023.
- Crosstalk contamination (F-039).
- A genuine population difference (skill, sex, club).
- A genuine unresolved dispute in the literature (F-011).

Each contradiction is resolved to one of these causes or recorded as unresolved. **Contradictions are never
averaged away.**

## Stage 6 — Bounded inference for never-measured muscles

~66% of zones have no data. For these, permitted inference only:

- **Mechanical necessity.** The lead foot resists 17–19 Nm of ground torque and carries ~95% bodyweight
  40 ms before impact. Muscles that must contribute to that are active. The *fact* is evidenced; the
  *magnitude* is bounded, not precise.
- **Anatomical obligation.** If a joint demonstrably moves in a direction and only muscle X can produce it,
  X was active.
- **Analogue transfer.** Data from a comparable rotational or weight-shifting task, clearly labelled as
  transferred, never presented as golf data.

Every Stage 6 record carries `inference: true`, its derivation, and a wider uncertainty band than any
measured record. **No Stage 6 record may ever render identically to a measured one** (F-009).

## Stage 7 — Validation by hold-out

**The stage that determines whether any of this is trustworthy.**

- Withhold a muscle that *does* have good measured data — trail gluteus maximus, or the wrist flexors.
- Reconstruct its activation curve using only Stages 4–6, from constraints and the other muscles.
- Compare the reconstruction against the withheld measurement.
- Repeat across several muscles spanning different regions and confidence tiers.

The agreement achieved is the honest accuracy figure for every Stage 6 inference in the app. If it is poor,
the inference layer is reduced or dropped rather than shipped. This directly answers the question the
inverse-dynamics literature raises, using our own data instead of assuming an answer.

## Stage 8 — Freeze and publish the dataset

- Version the dataset; the app consumes it as a build artefact.
- Every rendered value traceable to its records and their sources.
- Publish the uncertainty alongside the value, always.

## Sequencing and dependencies

```
Stage 0 Schema ─┬─> Stage 1 Units ──┐
                └─> Stage 2 Timeline ┴─> Stage 3 Envelopes ─> Stage 4 Chain ─> Stage 5 Audit
                                                                                    │
                                              Stage 6 Inference <───────────────────┘
                                                        │
                                              Stage 7 Validation ─> Stage 8 Freeze
```

Stages 1 and 2 are independent of each other and can run in parallel once the schema exists. Everything else
is strictly sequential — Stage 4 cannot run before the kinematics of Stage 2 are registered, and Stage 7 is
meaningless before Stage 6.

**Research continues in parallel throughout.** The programme is designed so new sources are transcribed into
the Stage 0 schema and flow through without restarting anything.
