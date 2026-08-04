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

## Phase 0 — Project initialisation
- T-001 Project autonomy settings (.claude/settings.json) — DONE 2026-08-04
- T-002 PROJECT_RULES.md with lifecycle skill bindings — DONE 2026-08-04
- T-003 Buildable Compose scaffold (debug + minified release verified) — DONE 2026-08-04
- T-004 Public GitHub repo EmperorKabir/Golf-Muscle created, initial push — DONE 2026-08-04
- T-005 Task-tracking system (this file + PROJECT_RULES.md pointer + memory index) — DONE 2026-08-04
- T-006 Record user answers Q-001..Q-008 as decisions D-001..D-007 — DONE 2026-08-04

## Phase 1 — Research and definition
- T-011 Maximum-breadth research into golf-swing muscle activation (EMG literature and all other available sources), cross-referenced, with citations. Output: `docs/research/` — IN PROGRESS
  - T-011a Swing phase taxonomy and timing (durations, kinematic sequence, transition) — IN PROGRESS
  - T-011b Trunk/core activation by phase — IN PROGRESS
  - T-011c Lower-limb and hip activation by phase, weight shift, ground reaction — IN PROGRESS
  - T-011d Shoulder girdle, arm, forearm and grip activation by phase; lead/trail asymmetry — IN PROGRESS
  - T-011e Modulation by club, shot type, skill level, tempo, and anthropometry (height, femur/limb length) — IN PROGRESS
  - T-011f Method for converting published %MVC values into a continuous 0–1 activation timeline — IN PROGRESS
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
