# Golf Muscle — Task List (single source of truth)

## Protocol (binding)
- This file is the single source of truth for all project work. Read it in full at every session start.
- Before starting ANY task: find its entry here, or add one first. No work happens without an entry.
- On finishing a task: update its status immediately, in the same working session.
- All new relevant information (user answers, decisions, spec changes) is recorded here the moment it arrives.
- Tasks are never deleted and never silently dropped. Only status transitions: TODO → IN PROGRESS → DONE (or BLOCKED with the exact blocker stated).
- Enforcement is three-layered so no session can miss it: (1) this file; (2) a binding pointer in PROJECT_RULES.md, which auto-loads every session; (3) the persistent memory index. If any layer is found missing, restore it before other work.

## Product specification (user, 2026-08-04)
- Android app: interactive 3D model of a human body performing a golf swing.
- Gestures: pinch to zoom; tap and drag to move the model (exact rotate vs pan mapping — see Q-005).
- Time slider at the bottom spanning the swing from address to follow-through. User can play the swing through, scrub to any point, and watch in slow motion — understanding muscle use over time, not just at static points.
- At any point in time, muscles are colour-coded on the 3D model with a gradient: red = most intense activation, blending down to transparent = zero use at that instant. Colour intensity corresponds to activation/exertion of that muscle at that moment in the swing.
- The 3D model must look good from all angles.
- Muscle grouping granularity: not so few that relevantly different muscles are merged; not so many that it reads like a biology textbook or splits groups below swing-relevance. When unsure, err toward MORE groups — unused muscles are useful contrast against the ones doing the work.
- Personalisation dimensions to design for (later): limb length, height, sex, shot type, club.
- Version 1 fixed subject: 189 cm tall male with long femurs, hitting an 8-iron.

## Open questions (asked 2026-08-04 — answers pending)
- Q-001 Muscle-effort data source: published measurement studies, a sports-science model, or expert estimate to start? — PENDING
- Q-002 Body appearance: anatomy-figure style (muscles visible, no skin) vs normal body with muscles glowing through? — PENDING
- Q-003 Does the figure animate through the swing motion, or hold a pose while only colours change over time? — PENDING
- Q-004 3D model sourcing: paid asset, free asset, or custom-built? Any budget? — PENDING
- Q-005 Gesture mapping: one-finger drag = spin the body; two-finger drag = slide it around the screen? — PENDING
- Q-006 Minimum phone: acceptable to drop very old/cheap phones (~pre-2018) for visual quality? — PENDING
- Q-007 Business model: free, paid, or free with extras? — PENDING
- Q-008 Right-handed golfer only for version 1? — PENDING

## Phase 0 — Project initialisation
- T-001 Project autonomy settings (.claude/settings.json) — DONE 2026-08-04
- T-002 PROJECT_RULES.md with lifecycle skill bindings — DONE 2026-08-04
- T-003 Buildable Compose scaffold (debug + minified release verified) — DONE 2026-08-04
- T-004 Public GitHub repo EmperorKabir/Golf-Muscle created, initial push — DONE 2026-08-04
- T-005 Task-tracking system (this file + PROJECT_RULES.md pointer + memory index) — DONE 2026-08-04

## Phase 1 — Discovery (blocked on user answers)
- T-010 Record user answers to Q-001..Q-008 here; update spec accordingly — BLOCKED (awaiting user reply)
- T-011 Research muscle activation data for a golf swing (8-iron, male) fitting the chosen data source; document sources with citations — TODO
- T-012 Define the muscle-group list at swing-relevant granularity (err toward more groups), with rationale per group — TODO
- T-013 Choose and validate the 3D rendering approach on Android (engine/library) via Context7 + a spike that renders and orbits a test mesh on device — TODO
- T-014 Source/produce the v1 body model (189 cm male, long femurs) meeting the looks-good-from-all-angles bar — TODO

## Phase 2 — Core app (sequenced after Phase 1 decisions)
- T-020 Time-slider architecture: swing timeline (address → follow-through), scrubbing, playback, slow motion — TODO
- T-021 Per-muscle colour mapping: activation value → red-to-transparent gradient shading on the model — TODO
- T-022 Gesture system: pinch zoom + drag interactions per Q-005 answer — TODO
- T-023 Swing motion/pose handling per Q-003 answer — TODO
- T-024 Responsive + foldable layout for the viewer and slider across all form factors — TODO
- T-025 On-device diagnostics via android-diagnostic-logger before first device test — TODO
