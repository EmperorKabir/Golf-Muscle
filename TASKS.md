# Golf Muscle — Task List (single source of truth)

## Protocol (binding)
- This file is the single source of truth for all project work. Read it in full at every session start.
- Before starting ANY task: find its entry here, or add one first. No work happens without an entry.
- On finishing a task: update its status immediately, in the same working session.
- All new relevant information (user answers, decisions, spec changes) is recorded here the moment it arrives.
- Tasks are never deleted and never silently dropped. Only status transitions: TODO → IN PROGRESS → DONE (or BLOCKED with the exact blocker stated).
- Enforcement is three-layered so no session can miss it: (1) this file; (2) a binding pointer in PROJECT_RULES.md, which auto-loads every session; (3) the persistent memory index. If any layer is found missing, restore it before other work.

## Product specification
### Core concept (user, 2026-08-04)
- Android app: interactive 3D model of a human body performing a golf swing.
- Gestures: pinch to zoom; **one finger spins the model** (orbit). Confirmed 2026-08-04.
- Time slider at the bottom spanning the swing from address to follow-through. User can play the swing through, scrub to any point, and watch in slow motion — understanding muscle use over time, not just at static points.
- At any point in time, muscles are colour-coded with a gradient: red = most intense activation, blending down to transparent = zero use at that instant. Intensity corresponds to that muscle's activation/exertion at that moment.
- The model must look good from all angles.
- Muscle grouping granularity: not so few that relevantly different muscles are merged; not so many that it reads like a biology textbook or splits groups below swing-relevance. When unsure, err toward MORE groups — unused muscles are useful contrast.
- Personalisation dimensions to design for (later): limb length, height, sex, shot type, club.
- V1 subject: 189 cm male, long femurs, 8-iron, right-handed.

### Decisions locked 2026-08-04 (user answers)
- **D-001 Accuracy is the project's highest priority.** Muscle-activation data must be researched from as many sources as possible — everywhere available — then reasoned into an applied model. Requires cross-referencing many independent sources for a full, well-rounded understanding of which muscles fire, at what intensity, at what time in the swing, and how activation ramps up/backs off across swing, golfer and club. Context efficiency is expected in gathering this.
- **D-002 Visual style: transparent artist's-mannequin wireframe.** Like a wooden posable artist's figure, except the wood itself is transparent and only the *borders* of each muscle zone are drawn as single-wire outlines. Colour fill appears only where a muscle is active. Zone borders are anatomically correct — real muscle boundaries, not simplified geometric shapes. NOT a full medical model: skin, sinew and tendons are irrelevant and excluded. Aesthetic serves comprehension of the swing, nothing else.
- **D-003 The figure animates through the full swing.** Body moves — arms, hips, spine — while colours change. Rationale (user): the user must be able to internalise which muscles fire at a given pose they can physically replicate. Applies to all swing types/clubs/golfers. Accepted as a large build.
- **D-004 The 3D model is generated in-project, not sourced.** Accepted as a large build. Gate before committing to it: produce at least 10 static-view renders viewable in a browser tab, each with bullet-pointed features and differences, for user selection.
- **D-005 Modern devices only.** Phones and tablets; no support obligation for old/low-end hardware. Visual quality takes precedence.
- **D-006 Free app.** No paid tiers.
- **D-007 Right-handed for V1.** Left-handed is a whole-system mirror and treated as straightforward once the right-handed path exists — not a separate build.

### Research findings that constrain the spec (added as they land — each needs a user decision or a labelled assumption)
- **F-001 Activation exceeds 100% MVC in the golf swing.** Erector spinae means reach 83–106% MVC in acceleration (Marta et al. 2013; J Sports Sci 2018). Isometric MVC underestimates ballistic activation across sports (giant slalom 283%, baseball pitching 226% — Clarys et al. 2010). **Consequence:** the colour scale must not hard-clip at 100%. Needs an explicit decision on ceiling and saturation behaviour. Source: `docs/research/06-activation-curve-and-colour-method.md`.
- **F-002 Club barely changes trunk activation.** Direct EMG comparison across driver/4-iron/7-iron/pitching wedge found **no significant trunk activation difference** (p>0.05). Lower-limb activation does vary by club, but non-monotonically (4-iron > pitching wedge; driver never shown to exceed irons). **Consequence:** club personalisation can confidently modulate kinematics and timing, but activation magnitude only as a labelled inference. Source: `docs/research/05-club-shot-golfer-and-anthropometry.md`.
- **F-003 No golf-specific evidence exists for femur length effects.** Zero peer-reviewed sources link femur length or leg-to-torso ratio to golf swing mechanics or muscle demand. Only cross-domain, non-peer-reviewed strength-training inference is available. **Consequence:** the V1 subject's defining "long femurs" trait cannot be evidence-based. It must be modelled from first principles and labelled in-product as modelled, not measured. Source: `docs/research/05-club-shot-golfer-and-anthropometry.md`.
- **F-004 No iron-specific swing timing data exists.** All published phase durations are driver-based (backswing ≈730–850 ms, downswing ≈230–300 ms, ratio ≈3:1). Any 8-iron timing must be scaled from driver data and labelled an unverified assumption. Source: `docs/research/T-011a-phase-taxonomy-and-timing.md`.
- **F-005 A pure red-to-transparent ramp fails accessibility and mid-range discrimination.** Red-green colour deficiency affects up to 8% of people; flat-luminance red gradients collapse to indistinguishable shades (Crameri et al., Nature Communications 11:5444, 2020). **Consequence:** retain the red-hot metaphor but pair it with a monotonic luminance ramp. Awaiting user decision via study 10 of the model style studies. Source: `docs/research/06-activation-curve-and-colour-method.md`.
- **F-006 Partial and full swings share one sequencing strategy.** Proximal-to-distal sequencing held across partial wedge shots and full swings, both sexes, both skill tiers (n=45, Sports Biomechanics 2010). **Consequence:** shot-length personalisation scales amplitude and timing only — the sequence pattern is not re-modelled per shot. Source: `docs/research/05-club-shot-golfer-and-anthropometry.md`.
- **F-008 "Acceleration phase" means opposite things in two literatures.** Peer-reviewed golf EMG (Bechler, Watkins, Pink/Jobe/Perry, Marta) defines acceleration as **impact → early follow-through** (i.e. *after* impact). Coaching sources including TPI use it for the final part of the downswing *before* impact. Any phase-averaged figure labelled "acceleration" is ambiguous until its source is checked. **Consequence:** adopt the peer-reviewed convention internally; user-facing labels must avoid the word entirely and say "just before impact" / "just after impact". Mixing the two would silently corrupt the timeline. Source: `docs/research/03-lower-limb-and-hip-activation.md`.
- **F-009 "Never measured" must not render as "not working".** Five lower-limb muscles have zero golf EMG data anywhere: gluteus minimus, the deep hip external rotators, tensor fasciae latae, soleus in isolation, and iliopsoas — the last gap explicitly confirmed in print by Marta et al. 2012. Under the current colour system an unmeasured muscle would be drawn transparent, which asserts to the user that it does no work in the golf swing. That is a false claim and directly undermines D-001. **Consequence:** the renderer needs a third visual state distinct from both "active" and "inactive" — the muscle zone outline present but marked as unmeasured. Affects T-012, T-014 and T-021. Raised from the research, not from the user's brief.
- **F-010 Published %MVC figures use three incompatible units.** %MMT (manual muscle test — Pink/Jobe/Perry/Watkins), %MVC (isometric max — Sorbie, Li, Cole & Grimshaw) and %EMGmax (peak within the swing — Marta). A muscle at "60%" in one study is not comparable to "60%" in another. **Consequence:** the activation model cannot pool raw published numbers; T-012 must define a conversion or segregation strategy before any value reaches the renderer. This is the single largest obstacle to a unified model. Source: `docs/research/02-trunk-and-core-activation.md`.
- **F-011 Erector spinae magnitude is genuinely disputed, by 2–3×.** Li et al. 2023 report 13–52% MVC across phases; Sorbie et al. 2018 report 67–106% MVC for the same muscle group. Not reconcilable from the published methods (different electrode sites, skill mixes, MVC references). **Consequence:** carry both ranges and show uncertainty rather than picking one. Affects the single most prominent muscle group in the back view. Source: `docs/research/02-trunk-and-core-activation.md`.
- **F-012 Highest verified activation anywhere in the swing: trail gluteus maximus, 62–72% EMGmax** (Marta et al. 2013), narrowly ahead of trail external oblique at 59–67%. Both peak forward swing → acceleration. **Consequence:** these two set the top of the colour scale for muscles with trustworthy numbers — and both are posterior, invisible in the current front-only style studies.
- **F-013 Three more muscles have zero golf EMG data**, confirmed by three independent research passes: transversus abdominis, multifidus, quadratus lumborum. Internal oblique is a near-gap (measured but amplitude never reported). Latissimus dorsi has **no numeric value at any phase** in any accessible source — qualitative timing only, despite being described as the primary power contributor of the early downswing. Extends F-009's unmeasured-state requirement to the trunk.
- **F-014 The literature never measures address, top of backswing, or impact.** All five-phase studies treat these as boundary *instants*, not sampled bins. **Consequence:** any value the app displays at address or impact — including the moment users will most want to inspect — is interpolation, not measurement, and must be presented as such. Source: `docs/research/02-trunk-and-core-activation.md`.
- **F-007 Draw/fade is distal, not trunk.** Swing path and lead-forearm supination differ significantly between shapes; pelvis and thorax rotation do not. **Consequence:** shot-shaping affects forearm activation, not core. Source: `docs/research/05-club-shot-golfer-and-anthropometry.md`.

## Phase 0 — Project initialisation
- T-001 Project autonomy settings (.claude/settings.json) — DONE 2026-08-04
- T-002 PROJECT_RULES.md with lifecycle skill bindings — DONE 2026-08-04
- T-003 Buildable Compose scaffold (debug + minified release verified) — DONE 2026-08-04
- T-004 Public GitHub repo EmperorKabir/Golf-Muscle created, initial push — DONE 2026-08-04
- T-005 Task-tracking system (this file + PROJECT_RULES.md pointer + memory index) — DONE 2026-08-04
- T-006 Record user answers Q-001..Q-008 as decisions D-001..D-007 — DONE 2026-08-04

## Phase 1 — Research and definition
- T-011 Maximum-breadth research into golf-swing muscle activation (EMG literature and all other available sources), cross-referenced, with citations. Output: `docs/research/` — IN PROGRESS
  - T-011a Swing phase taxonomy and timing (durations, kinematic sequence, transition) — DONE 2026-08-04 (`docs/research/T-011a-phase-taxonomy-and-timing.md`; several sub-findings flagged unverified — iron-specific durations, some ms-level segment-peak offsets, provenance of a few secondary citations — see file's "Open verification gaps")
  - T-011b Trunk/core activation by phase — DONE 2026-08-04 (`docs/research/02-trunk-and-core-activation.md`)
  - T-011c Lower-limb and hip activation by phase, weight shift, ground reaction — DONE 2026-08-04 (`docs/research/03-lower-limb-and-hip-activation.md`)
  - T-011d Shoulder girdle, arm, forearm and grip activation by phase; lead/trail asymmetry — IN PROGRESS
  - T-011e Modulation by club, shot type, skill level, tempo, and anthropometry (height, femur/limb length) — DONE 2026-08-04 (`docs/research/05-club-shot-golfer-and-anthropometry.md`)
  - T-011f Method for converting published %MVC values into a continuous 0–1 activation timeline — DONE 2026-08-04 (`docs/research/06-activation-curve-and-colour-method.md`)
- T-012 Define the muscle-group list at swing-relevant granularity (err toward more), rationale per group — TODO
- T-013 Choose and validate the Android 3D rendering approach (Context7 + on-device spike rendering and orbiting a test mesh) — TODO
- T-014 Generate the V1 body model (189 cm male, long femurs) in the D-002 style, meeting the all-angles bar — TODO
- T-015 D-004 gate: 10 static-view render studies in a browser artifact with per-option bullet points, for user selection — IN PROGRESS

## Phase 2 — Core app
- T-020 Time-slider architecture: swing timeline (address → follow-through), scrubbing, playback, slow motion — TODO
- T-021 Per-muscle colour mapping: activation value → red-to-transparent gradient shading — TODO
- T-022 Gesture system: pinch zoom + one-finger orbit (D-002/Q-005 confirmed) — TODO
- T-023 Full swing animation of the figure (D-003) — TODO
- T-024 Responsive + foldable layout for viewer and slider across all form factors — TODO
- T-025 On-device diagnostics via android-diagnostic-logger before first device test — TODO
- T-026 Left-handed mirror mode (D-007) — TODO
- T-027 Personalisation parameters: height, limb/femur length, sex, club, shot type — TODO
