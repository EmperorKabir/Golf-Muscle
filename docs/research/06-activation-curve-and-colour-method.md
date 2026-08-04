# Converting published EMG into a continuous activation timeline, and mapping it to colour

Scope: how to turn phase-averaged %MVC values from the literature into the smooth 0–1 curves the time
slider needs, and how to map those onto colour. Every numeric claim carries a source. Areas where the
literature does not settle the question are marked as judgement calls rather than papered over.

## 1. What %MVC means, and why it exceeds 100% in a golf swing

- %MVC = (EMG amplitude during task ÷ EMG amplitude during a maximal voluntary contraction) × 100.
  Normalising removes inter-subject and inter-muscle scaling differences — electrode placement,
  subcutaneous fat, skin impedance, muscle size — making amplitudes comparable across people and muscles.
  Sources: *Impact of Normalization Procedures on sEMG Data Integrity*, Sensors 25:2668, 2025
  (https://www.mdpi.com/1424-8220/25/9/2668); Besomi et al., CEDE Amplitude Normalization Matrix,
  J Electromyogr Kinesiol 53:102438, 2020.
- MVC reference collection: maximal isometric effort in a standardised joint position near the
  torque-angle optimum, peak or plateau amplitude over 3–5 s, often averaged over 2–3 trials.
  Sources: PeerJ 2025 (https://peerj.com/articles/20848/); Clarys et al., *Critical Appraisal and Hazards
  of Surface EMG in Sport and Exercise*, 2010 (PMC3289173).
- CEDE consensus (Besomi et al. 2020) ranks six normalisation references by task-specificity:
  (1) MVC in the same task, (2) standardised isometric MVC, (3) standardised submaximal task,
  (4) peak/mean EMG within the task, (5) non-normalised, (6) maximal M-wave.

### Values above 100% MVC are expected, not error

Isometric MVC systematically **underestimates** true peak activation in fast stretch-shortening-cycle
movements. Clarys et al. (2010) tabulate peak dynamic EMG as a percentage of the static MVC reference:

| Task | Peak EMG as % of static MVC |
|---|---|
| Giant slalom | 283% |
| Baseball pitching | 226% |
| Sculling | 195% |
| Special slalom | 180% |
| Back-stroke swimming | 142% |
| Front-crawl swimming | 138% |
| Archery | 111% |

Clarys et al. state directly that "statically obtained EMG cannot create a reference for dynamic-,
ballistic- and complex EMG. It would be physiologically and biologically incorrect."

**Golf-specific confirmation.** Marta et al., Sports Engineering 8(4):779, 2013
(https://doi.org/10.1260/1747-9541.8.4.779) report thoracic and lumbar erector spinae at **67–99% MVC in
the forward-swing phase and 83–106% MVC in acceleration** — the *mean* crosses 100% in acceleration.
Right external oblique and trailing-leg gluteus maximus reach 59–72% in the same phases.

Causes of supramaximal values: MVC test-position mismatch against the dynamic task, contraction-type
difference (isometric reference vs concentric/eccentric/SSC task), subject motivation during the MVC,
movement velocity, stretch-shortening-cycle potentiation, and electrode cross-talk. Corroborated outside
golf by *Voluntary contractions underestimate peak muscle activity in drop jumps* (PMC12152988).

**Consequence for this app:** the colour scale's domain must not hard-clip at 100%. Either extend the
domain to an empirically observed ceiling (roughly 120–150% based on the source studies' reported ranges)
or soft-saturate above 100% — and document it, so a saturated muscle is not mistaken for a rendering bug.

## 2. Signal processing: raw EMG to a usable envelope

- Acquisition band: 10–20 Hz high-pass, ≥500 Hz low-pass, sampling ≥1000 Hz. SENIAM — Hermens et al.,
  J Electromyogr Kinesiol 10:361, 2000.
- Full-wave rectification is universal before smoothing.
- Linear envelope = rectified signal low-pass filtered. Published cutoffs span 3–10 Hz, most commonly
  **6 Hz**, using a low-order (2nd–4th) zero-lag dual-pass Butterworth, per Winter's gait-EMG methodology.
  Faster upper-limb muscles are sometimes filtered at 6–12 Hz.
- RMS alternative: moving-window RMS with a **50 ms** window is the SENIAM-consistent norm; working range
  50–100 ms. Amplitude attenuation and onset-time shift both grow with window length — a real problem for
  fast-rising ballistic bursts. Source on onset-shift: Physiol. Meas. 2021
  (https://iopscience.iop.org/article/10.1088/1361-6579/abef56).

**Recommended for this project:** full-wave rectify, then 6 Hz 4th-order zero-lag Butterworth (or 50 ms
RMS — broadly equivalent in the golf-swing bandwidth). Do not exceed ~10 Hz cutoff or ~100 ms RMS window,
or the downswing burst gets blunted and delayed. The trade-off is explicit and unresolved by consensus:
smoother settings give a more plausible bell-shaped envelope but lag and flatten the peak; sharper
settings keep timing fidelity but produce noisier colour transitions. No SENIAM or ISEK document
prescribes a single correct value for ballistic sport envelopes — this is a design choice inside the
3–10 Hz / 50–100 ms consensus band.

## 3. Electromechanical delay

EMD is the lag between EMG onset and measurable force onset, covering synaptic transmission,
action-potential propagation, excitation-contraction coupling, and series-elastic-component stretch.
Sources: PubMed 506761; PMC4274888; PMC3537731; J Appl Physiol 2009 (very-high-frame-rate ultrasound).

| Muscle / condition | EMD |
|---|---|
| Gastrocnemius (electrically stimulated) | 11.6 ± 1.5 ms |
| Quadriceps (voluntary isometric) | 49.7 ± 7.0 ms |
| Biceps brachii (voluntary concentric) | 41 ± 13 ms |
| Triceps brachii (concentric) | 26 ± 11 ms |
| General literature range | ~10–100 ms |

No golf-specific or trunk-rotational EMD values were located. The values above are limb muscles and are
directionally indicative only.

**Decision required.** If the app's language is "activation" or "effort" (neural drive), leave the signal
unshifted. If it is framed as "force output", apply a uniform ~30–50 ms forward shift and disclose it as
an approximation — EMD is muscle-, contraction-type-, velocity- and fatigue-dependent, and applying one
generic offset to muscles whose true EMD is unmeasured is an unvalidated assumption.

## 4. Turning phase means into a continuous curve

The problem: golf EMG papers report **one mean %MVC per swing phase**, not a continuous trace. A smooth
colour gradient needs interpolation between those means.

### Candidate methods

- **PCHIP / monotone cubic Hermite** — shape-preserving: no overshoot, no spurious oscillation, preserves
  monotonicity within each interval, reproduces local extrema exactly at data points. The physiological-data
  literature explicitly favours monotone-preserving interpolants because ordinary cubic splines "can exhibit
  artifacts of overshooting, undershooting, or unwanted oscillations... that can misrepresent what the data
  actually says". Sources: MATLAB pchip documentation; Xuefeng Xu, *Monotone Piecewise Cubic Interpolation*;
  *Monotone Data Visualization via Rational Trigonometric Spline* (PMC3998008).
- **Natural/clamped cubic spline** — smoother C² continuity but overshoots beyond the local range of
  adjacent phase means, which for a %MVC quantity generates implausible spikes and troughs.
- **Catmull-Rom** — passes through control points, cheap, C¹, standard in graphics keyframe animation.
  No monotonicity or overshoot constraint, and no physiological grounding. It is a graphics convenience,
  not a validated method for reconstructing physiological amplitude. Centripetal parameterisation (α = 0.5)
  reduces but does not eliminate cusping.
- **Gaussian / bell basis per burst** — model each burst as a(t) = A·exp(−(t−μ)²/2σ²). Grounded in real
  practice: Gaussian mixture models are used to decompose sEMG envelopes into onset/offset components
  (PMC4928879; PMC4454555; PMC5481033). Caveat: real EMG bursts are **asymmetric** — faster rise than
  decay — so a symmetric Gaussian is a simplification; ex-Gaussian, gamma, or unequal σ_rise/σ_fall is
  more faithful to the triphasic ballistic pattern.

### Constraints a defensible method must satisfy

1. **Non-negativity** — %MVC cannot go below zero. PCHIP guarantees this by construction; natural splines
   and Catmull-Rom do not.
2. **No overshoot** beyond the adjacent data range, so the curve never implies a peak the source never
   reported.
3. **Mean preservation under integration** — the frequently missed one. A published phase mean is a
   definite-integral average over that phase's real duration: (1/(t₁−t₀))·∫a(t)dt = reported %MVC. Placing
   that value as a node at the phase midpoint does **not** guarantee the fitted curve integrates back to it.
   Purpose-built mean-preserving (interval-preserving) splines exist for exactly this bin-average problem:
   *Mean-preserving interpolation with splines for solar radiation modelling*, Solar Energy 2022;
   *A Fast Mean-Preserving Spline for Interpolating Interval Data*, J. Atmos. Ocean. Technol. 39(4), 2022.
   (Author attribution unverified for both — full text was inaccessible. Cite by title/journal/year.)

The numerical-analysis literature notes that satisfying non-negativity, monotonicity **and** exact mean
preservation simultaneously with one low-order piecewise polynomial is generally not possible — some
accuracy trade-off is unavoidable (GMD 11:2503, 2018).

### Verdict

**Use a monotone, shape-preserving construction (PCHIP family, ideally mean-preserving) treating each
phase mean as an interval average rather than a point sample.** This addresses the two failure modes most
damaging to credibility: overshoot beyond physiologically observed bounds, and misrepresenting what the
published mean actually measured. Catmull-Rom is the weakest option scientifically and is acceptable only
as a rendering-layer smoothing pass over an already-correct base curve, never as the primary reconstruction.

**Priority source material:** many phase-mean papers also publish an averaged full-trace figure alongside
the phase table. Where one exists, digitise the figure in preference to interpolating the table — it
recovers intra-phase dynamics the table cannot.

**Standing honesty constraint:** interpolating between phase means cannot recover intra-phase peaks. The
83–106% acceleration figure from Marta et al. is itself already an average and may understate a higher
instantaneous peak inside that phase. The reconstructed curve must be documented as a smoothed
approximation of reported phase averages, not a recovered original signal.

## 5. Onset, offset, and burst shape

- Threshold detection: flag onset when the smoothed signal exceeds baseline **mean + k·SD** for a minimum
  sustained duration. Hodges & Bui (1996, PubMed 9020824) compared 27 variants — filtering at 10/50/500 Hz
  crossed with thresholds of 1, 2 or 3 SD sustained for 20, 50 or 100 ms. Common practice is 1–3 SD; some
  protocols use 3 SD sustained for ≥25 consecutive samples.
- **Thresholds should differ by phase.** Physiol. Meas. 2021 found optimal detection thresholds differ by
  contraction type: h = 6 (SD-equivalent) minimised error for **explosive** contractions, h = 10 for
  **ramped**. The downswing is the explosive case and warrants the faster-responding threshold; address and
  backswing do not.
- Known failure mode: baseline noise biases onset time — low baseline gives false early onset, high
  baseline gives late or missed onset (PMC5425195).

### Burst timing in ballistic movement

| Measure | Value | Source |
|---|---|---|
| Time-to-peak, small ballistic contraction | ~80 ms | PubMed 745068 |
| Time-to-peak, strong ballistic contraction | ~150 ms | PubMed 745068 |
| Time-to-peak, soleus (slow muscle, any force) | ~150 ms | PubMed 745068 |
| Explosive isometric: rise to 100–130% of max voluntary EMG | ~75–100 ms | Buckthorpe et al., Muscle & Nerve 2012 |
| Minimum plausible burst duration | well under 50 ms | PMC7533965 |

Ballistic movement produces a **triphasic** agonist–antagonist–agonist burst pattern, not a single
monophasic burst (PubMed 7849654). A single bell per prime mover may therefore need a secondary smaller
antagonist burst to be physiologically complete — though phase-mean golf tables typically report only net
agonist activation. No golf-specific onset/offset threshold study was located; the values above are the
closest evidenced analogues and are order-of-magnitude guidance, not golf-validated constants.

## 6. Time normalisation — and why a 0–100% timeline is a trap

Established in the closely analogous gait literature: normalising a cycle to 0–100% assumes the *relative*
timing of sub-phases is constant. When it is not, "50% of the cycle" maps to different biomechanical events
in different trials, and averaging normalised curves mixes data from different true phases
(J. Biomech. 2024, https://www.sciencedirect.com/science/article/abs/pii/S0021929024003312).

Concrete demonstration: increasing gait speed reduces the absolute duration of every phase but **shifts
their percentage share** — loading response and pre-swing shrink as a proportion of the cycle while
mid/terminal stance and swing grow (J. Biomech. 2024). Percentage-of-cycle is speed-dependent, not a fixed
proportional map. Transferred to golf: a single 0–100% axis built from population-average phase boundaries
will misrepresent an individual swing's true rate of change.

**Solution — piecewise normalisation.** Normalise each phase independently to its own local 0–100%, then
concatenate, rather than normalising the whole swing to one global axis. This preserves each phase's
internal shape while still allowing cross-swing comparison.

**Playback architecture (directly relevant to the time slider).** No biomechanics source addresses this
engineering problem; the nearest is *Real-time Slow-motion Framework*, Augmented Humans 2024, which
establishes that real-time and slow-motion are "basically incompatible properties" unless deliberately
architected. Combining that with the gait literature gives a defensible rule:

- Drive the activation curve as a function of **true elapsed real time in milliseconds** within the actual
  modelled swing — not an abstract 0–100% index. The per-phase 0–100% mapping is used only to *place*
  interpolation nodes when reconstructing the curve from population phase means, never as the runtime clock.
- For slow motion, scale the **real-time clock** by a constant factor (e.g. 0.25×) rather than
  re-normalising over a percentage timeline. This preserves true relative durations, so a genuinely fast
  downswing still reads as proportionally fast against a slow backswing.
- Reserve whole-swing 0–100% normalisation for population comparison overlays only.

## 7. Mapping activation to colour

- Perceptually uniform colormaps are established best practice for quantitative magnitude. matplotlib
  adopted **viridis** as default from v2.0 specifically for its **monotonically increasing luminance**,
  exploiting that the eye is more sensitive to brightness than hue — which also makes it robust for readers
  with reduced colour perception. Sources: CRAN viridis vignette; Kenneth Moreland, *Color Map Advice for
  Scientific Visualization*.
- Empirical accuracy evidence: Liu & Heer, *Somewhere Over the Rainbow: An Empirical Assessment of
  Quantitative Colormaps*, ACM CHI 2018 — **viridis showed consistently low reading error; rainbow/jet was
  the most error-prone**; a single-hue sequential blue scale was read fastest.
- Crameri, Shephard & Heron, *The misuse of colour in science communication*, Nature Communications
  11:5444, 2020 — rainbow-like and red–green maps are both perceptually distorting (uneven gradients
  misrepresent equal data steps) and inaccessible to colour-vision-deficient readers. Recommends maps built
  with linear perceptual lightness progression.

### Linear vs non-linear mapping

- Brightness perception follows a power law (Stevens); greyscale can be power-transformed with γ ≈ 0.4 to
  approximate equal perceived-brightness steps.
- **However**, perceptually uniform colormaps are already constructed in a perceptually linear space
  (CIELAB / CAM02-UCS), so mapping data **linearly** onto the colormap index already yields uniform
  perceived steps. Stacking a data-domain gamma pre-warp on top would double-correct. Sources: Moreland;
  ColorCET / HoloViz.
- Whether to apply data-domain gamma or log compression to boost discriminability in a specific %MVC band
  is a live design choice with **no EMG-specific evidence either way**. Marked as a judgement call.

### The red-scale problem — this directly affects our chosen colour system

Red-green colour-vision deficiency affects up to **8%** of the population, predominantly male (ASCB
accessibility guide; Sigma). A smooth red gradient is precisely the failure case flagged by Crameri et al.:
under deuteranomaly or protanomaly it "may appear flat or muddied" and collapses to indistinguishable
shades.

**If red is retained** for the intuitive "red = maximal exertion" metaphor — which it should be, it is a
strong and widely understood signal — it must be **paired with a luminance ramp** (dark red → bright
yellow-orange, in the manner of inferno/magma) rather than a flat-luminance red hue ramp or a red–green
pair. This keeps the hot-red metaphor while remaining readable by brightness alone for colour-blind users,
satisfying Crameri et al.'s monotonic-lightness recommendation.

This is the evidence behind the warm-ramp option (study 10) in the model style studies.

## Recommended parameters

| Stage | Recommendation | Basis |
|---|---|---|
| Amplifier bandwidth | 10–20 Hz HP, ≥500 Hz LP | SENIAM / ISEK |
| Rectification | Full-wave | Universal |
| Envelope low-pass | 6 Hz (range 3–10), 2nd–4th order zero-lag Butterworth | Winter; SENIAM |
| RMS window (alternative) | 50 ms (range 50–100) | SENIAM |
| Onset threshold | Baseline mean + 1–3 SD; faster threshold for downswing/acceleration, slower for address/backswing | Hodges & Bui 1996; Physiol. Meas. 2021 |
| EMD offset | None if framed as activation; ~30–50 ms if framed as force, disclosed as approximation | Composite limb-muscle EMD studies |
| Phase-mean interpolation | Monotone / mean-preserving spline (PCHIP family), non-negative, no overshoot | Numerical analysis + physiological data literature |
| Playback time base | True elapsed milliseconds, uniformly scaled for slow motion; per-phase normalisation only for cross-swing comparison | Gait time-normalisation literature |
| Colour | Perceptually uniform ramp with monotonic lightness; map data linearly onto the ramp index; avoid flat-luminance red and red–green pairs | Crameri et al. 2020; Liu & Heer 2018 |

## Open judgement calls

These are genuinely unsettled in the literature and need an explicit product decision rather than a
default:

- Whether to offset the signal for electromechanical delay — no golf or trunk-muscle EMD values exist.
- Whether phase-mean reconstruction alone is acceptable, or full-trace source figures must be digitised
  wherever published. Phase means cannot recover intra-phase peaks.
- Interpolation node placement: phase midpoint (simpler, approximate) vs mean-preserving integral
  construction (correct, more complex).
- Data-domain gamma or log pre-scaling of %MVC before colour mapping — no EMG-specific evidence found.
- Clipping behaviour above 100% MVC. No standard convention exists in the visualisation literature; must
  be an explicit decision, given golf erector spinae means reach 106%.
