# Foot, ankle and deep calf in the golf swing

Status: COMPLETE. 26 distinct primary/secondary sources cited (PMID or PMCID given for each),
covering all 10 required topics. Two dead ends confirmed and not retried per task instruction
(physio-pedia.com, teachmeanatomy.info were not needed — Europe PMC REST API and PMC/PubMed
HTML were sufficient for every topic).

Phase abbreviations follow project convention: ADD address, TA takeaway/early backswing, LB late
backswing, TOP top/transition, ED early downswing, LD/ACC late downswing–acceleration (pre-impact),
IMP impact, EFT early follow-through, LFT late follow-through. L = lead leg (left, right-handed golfer),
T = trail (right). **N/D = no data found.** No values are invented to fill gaps.

Context set by task: lead-foot vertical GRF peaks near 95% bodyweight ~40 ms before impact, with
17–19 Nm of free-moment (vertical-axis torque) at the lead foot. This document investigates what is
directly measured about foot/ankle musculature and pressure, and separately what can only be
inferred from that GRF/torque data.

---

## 1. Plantar pressure distribution during the golf swing

### Pataky, Mu, Bosch, Ball & Robinson 2015 — the strongest primary source found
**"Correlation between maximum in-shoe plantar pressures and clubhead speed in amateur
golfers"**, *Journal of Sports Sciences* (2015), PMID 25010946, DOI
10.1080/02640414.2014.932917. Free full text PDF (Shinshu University repository):
https://soar-ir.repo.nii.ac.jp/record/13300/files/Correlation_between_maximum_in-shoe.pdf

**Methods**: N=32 right-handed male amateur golfers, age 45.2±13.1 y, height 176.2±6.0 cm,
mass 76.4±7.7 kg, handicap 2.7–25 (mean 15.8±6.2). Ten driver swings each off an artificial-turf
mat, all fitted with the same golf shoe model (Nike Lunarlon Control) to remove shoe effects.
In-shoe pressure: Pedar X insole system (Novel GmbH), 99 sensors/insole, 100 Hz, ~98% rated
accuracy. Clubhead speed: Flightscope X2 doppler radar (~99% rated accuracy). Maximum
plantar pressure (PP) extracted per sensor from a 2 s window centred on ball contact. Statistical
parametric mapping (SPM) used for whole-foot, spatially continuous inference (validated
methodology per Pataky 2008, J Biomech 41(11):2464–2473).

**Peak pressure values (Fig.2, group-average maxima, colour scale 0–150+ kPa)**: highest
**target(lead)-foot** pressures at the **lateral forefoot, heel, and hallux**; highest **back(trail)-foot**
pressures at the **medial forefoot and hallux** — an asymmetric, side-specific loading pattern.
Individual subject maxima (Fig.3) ranged roughly **0–200+ kPa** across the foot, with the fastest
swingers (46.5–49.2 m/s clubhead speed, 82.0–88.5 kg) showing markedly higher and more
concentrated lateral target-forefoot and hallux pressures than the slowest swingers (29.4–34.2
m/s, 68.0–80.0 kg).

**Correlation with clubhead speed**: single-sensor example at lateral target-forefoot: **r=0.632,
t=4.469, p=0.000** (linear regression across subjects, clubhead speed 29.4–49.2 m/s vs. pressure
0–~210 kPa at that sensor). Whole-foot SPM: significant positive correlations (α=0.05, critical
|t|=3.58, df=30) confined to the **lateral target(lead)-foot and the very distal back(trail)-foot**;
weak, non-significant negative correlations on the posterior back-foot and on the posterior heel
and medial forefoot of the target-foot. Body mass vs. clubhead speed: r=0.315, p=0.079 (n.s.).
Within-subject (trial-to-trial) PP–clubhead-speed correlation: **not significant** (reported but not
tabulated) — between-subject effects only.

**Interpretation offered by the authors**: target-foot loading *location*, not just magnitude, may be
as important as total weight-transfer for clubhead speed; "neither ground reaction force nor COP
can reveal which parts of the foot should be loaded" and "COP data are anatomically ambiguous
because one COP location can be produced by many PP distributions" — i.e. plantar-pressure
mapping carries information COP time-series cannot.

**Cited prior findings reproduced/contrasted within this paper** (chain of citations, not
independently verified against original text unless noted):
- Chu, Sell & Lephart 2010 (*J Sports Sci* 28(11):1251–1259) and Okuda, Gribble & Armstrong
  2010 (*J Sports Sci Med* 9:127–133): increased **target(lead)-foot loading and decreased
  back(trail)-foot loading ~40 ms prior to ball contact** in more skilled golfers — this is the same
  40 ms pre-impact timing window named in the task's GRF context, now corroborated from an
  independent citation chain.
- Richards, Farrell, Kent & Kraft 1985 (*Res Q Exerc Sport* 56:361–365): target-foot **heel**
  loaded through ball contact; higher target-foot forces in skilled golfers.
- Ball & Best 2007 (*J Sports Sci* 25(7):771–779) and 2011 (*J Sports Sci* 29(6):587–590):
  skilled golfers show greater whole-body **COPy** (target-direction) excursion than less-skilled;
  "target-foot golfers" (more posterior COPx through impact) have lower average handicaps.
- Ball & Best 2012 (*Sports Biomech* 11(2):175–189): individual-based COP pattern analysis —
  large golfer-to-golfer variability in swing mechanics determinants.
- Murakami & Mochimaru 2010 (Proc. 6th World Congress of Biomechanics): spatially continuous
  foot pressure + GRF + 3D motion for spikeless shoe development; single-digit handicappers load
  the **posterior and lateral target-foot**.
- Kawashima, Meshizuka & Takeshita 1998 (Science and Golf III): discrete-sensor kinematic study
  — **heel and hallux** forces (not lateral forces) associated with more skilled golfers — partially
  contradicts the present SPM result, discussed as possibly a handicap-range effect (that study used
  handicap <10 only).
- Wallace, Grimshaw & Ashford 1994 (Science and Golf II, pp.25–32): discrete pressure profiles —
  medial target-foot pressure associated with skilled golfers' longest drives — also partially
  contradicted by the present lateral-foot finding.
- Healy 2009 (MSc thesis, Dublin City University): barefoot testing found **no COPx difference**
  between <3 and 10–18 handicap golfers — the present paper notes this barefoot protocol likely
  altered foot stability/friction relative to shod testing, a first hint that barefoot vs shod changes
  foot-loading strategy (see §8 below).
- Rambarran & Kendall 2001 (Proc. 5th Symposium on Footwear Biomechanics): passive **heel-lifts**
  increased within-subject driving distance — consistent with anterior/lateral pressure
  redistribution improving clubhead speed.
- Koenig, Tamres & Mann 1994 (Science and Golf II): shoe-ground interaction biomechanics
  (title only surfaced; not independently retrieved).

### Ozturk et al. 2019 — static and dynamic plantar pressure in elite (Turkish national team) golfers
**"Evaluation of foot pressure in national golfers"**, *Acta Orthop Traumatol Turc* (2019), PMID
30782452, PMCID PMC6506813, DOI 10.1016/j.aott.2019.02.005 (open access, full text retrieved).

**Methods**: N=8 elite junior golfers (3 female: age 15.33±0.57 y, height 167±3.61 cm, weight
59.3±11.71 kg; 5 male: age 17±0.83 y, height 177.2±8.61 cm, weight 72.8±15.61 kg), Turkish
National Team. Digital Biometry Images Scanning (DBIS) for postural analysis, Modular
Electronic Baropodometric platform for static/dynamic plantar pressure, Stabilometry for balance.

**Static plantar load values** (forefoot vs rearfoot, by sex and side):
- Forefoot surface/load/weight-ratio — Left: female 32.08 cm², 16.7 kg, 37.6%; male 46.05 cm²,
  21.9 kg, 47.8%. Right: female 40.4 cm², 22.7 kg, 40.2%; male 48.7 cm², 25.5 kg, 47.7%.
- Rearfoot surface/load/weight-ratio — Left: female 34 cm², 26.8 kg, 61.4%; male 44.6 cm²,
  24.5 kg, 52.1%. Right: female 37 cm², 33.8 kg, 63%; male 49.6 cm², 27.9 kg, 52.2%.
- Static foot angle: left 9.5° (female) / 12.5° (male); right 11° (female) / 15° (male).
- All forefoot/rearfoot surface, load, weight-ratio and foot-angle differences significant at p<0.05.

**Dynamic evaluation**: significant right/left foot surface and load differences (p=0.024–0.042
across sexes); dominant-foot values exceeded non-dominant-foot values (p<0.05).

**Composite indices**: Static BPI (postural index) mean 7 points (population norm 0–10); Dynamic
BPI mean 29 points (norm 0–20, i.e. markedly elevated — golfers show more dynamic postural
asymmetry than the general reference population); Stabilometric balance score mean 20 points
(norm 0–10, also elevated). The paper interprets elevated dynamic/balance indices as clinically
relevant to injury risk and performance, but does not further decompose them by swing phase.

### Kim et al. 2016 — predicting 6-axis ground reaction force/moment from plantar pressure
Study predicting 6-axis GRF (3-axis force + 3-axis moment) from in-shoe plantar pressure via
wavelet neural network. *J Biomech* 49(14):3153–3161 (2016), PMID 27515436, DOI
10.1016/j.jbiomech.2016.07.029 (subscription; abstract only). N=80 golf-swing subjects, 5-fold
cross-validation. Using accumulated plantar pressure + COP pattern + opposite-foot pressure as
combined inputs, prediction correlation with true force-plate GRF/moment reached **r=0.73–0.97**
(weaker input sets) up to **r=0.83–0.98** (full input set). This confirms plantar pressure
distribution and force-plate GRF/free-moment are tightly coupled (as expected mechanically) —
i.e. plantar pressure is a legitimate, validated proxy channel for the GRF and free-moment data
already in the model, reinforcing that the ~17–19 Nm free-moment and ~95% BW vertical GRF
figures have a real, measurable footprint in plantar pressure distribution, even though this study
does not decompose that footprint by anatomical foot region.

### Skill-level and technique comparison — Okuda, Gribble & Armstrong 2010 (full text retrieved)
**"Trunk Rotation and Weight Transfer Patterns Between Skilled and Low Skilled Golfers"**,
*J Sports Sci Med* 9:127–133 (2010), PMID 24149396, PMCID PMC3737954. N=13 skilled
(handicap 0.8±2.6, 14.1±4.9 y experience) vs N=17 low-skilled (handicap 30.8±5.5, 5.4±3.6 y
experience) golfers, full driver swings, force plates under each foot.

**Vertical GRF (VGRF, fraction of bodyweight, mean(SD)), lead foot**: address 0.50(0.06) low-
skilled / 0.48(0.08) skilled; backswing 0.35(0.11) low-skilled / **0.25(0.09) skilled** (p<0.05,
skilled unload the lead foot more in backswing); downswing 0.33(0.19) low-skilled / **0.59(0.28)
skilled** (p<0.01, skilled reload the lead foot earlier/more in the downswing); ball impact 1.05(0.23)
low-skilled / 0.90(0.28) skilled; follow-through 0.78(0.17) low-skilled / 0.68(0.21) skilled.
Maximum lead VGRF: 1.13(0.25) low-skilled / 1.09(0.32) skilled (n.s.) — **note: these ball-impact
and maximum lead-foot VGRF values (~90–113% BW) directly corroborate the task's stated ~95%
BW lead-foot peak, from an independent primary source.**

**Vertical GRF, trail foot**: address 0.51(0.05) low-skilled / 0.52(0.11) skilled; backswing
0.76(0.13) low-skilled / **0.92(0.12) skilled** (p<0.01); top of backswing 0.83(0.14) low-skilled /
0.74(0.12) skilled; downswing 0.67(0.18) low-skilled / 0.60(0.15) skilled; ball impact 0.25(0.16)
low-skilled / 0.38(0.20) skilled; follow-through 0.25(0.14) low-skilled / 0.36(0.19) skilled.
Maximum trail VGRF: 0.89(0.12) low-skilled / **0.98(0.09) skilled** (p<0.05).

**Trunk/pelvis rotation (context, not foot-specific but co-registered with the same GRF data)**:
upper-trunk horizontal rotation at backswing 40.7°(10.4) low-skilled / 47.8°(6.3) skilled (p<0.05);
at follow-through −55.2°(12.1) low-skilled / **−43.3°(10.5) skilled** (p<0.01). Pelvic horizontal
rotation at address −3.1°(4.4) low-skilled / 0.4°(1.5) skilled (p<0.01); at backswing 21.8°(10.8)
low-skilled / 28.8°(8.9) skilled (p<0.05); at downswing 20.7°(13.7) low-skilled / **10.1°(7.9)
skilled** (p<0.05, skilled complete pelvic rotation earlier, leaving less to do in the downswing
itself). Pelvic anterior-posterior tilt at ball impact 0.0°(8.1) low-skilled / 6.6°(5.2) skilled (p<0.05);
at follow-through 4.2°(7.9) low-skilled / 10.5°(5.8) skilled (p<0.05).

**Interpretation**: skilled golfers show earlier trunk rotation with rapid weight transfer to the trail
foot in the backswing, and earlier pelvic rotation with earlier weight transfer to the lead foot in
transition/downswing — i.e. skill separates *timing* of the weight shift more than its endpoint
magnitude. This is a proximal-to-distal-sequencing pattern structurally identical to the
lower-limb-leads-the-chain finding already documented for hip/knee EMG in
`03-lower-limb-and-hip-activation.md`.

### Chu, Sell & Lephart 2010 — large-N regression linking swing variables to ball velocity
**"The relationship between biomechanical variables and driving performance during the golf
swing"**, *J Sports Sci* 28(11):1251–1259 (2010), PMID 20845215 (not in PMC, abstract only).
N=308 golfers. Regression models at four swing events explained **44–74% of variance** in ball
velocity. Significant predictors: upper-torso–pelvis separation (X-Factor), delayed release of arms/
wrists, trunk forward and lateral tilt, and **weight-shifting** during the swing. This is the largest-N
study located in this whole document, and its inclusion of weight-shift as a significant ball-velocity
predictor (independent of the Pataky 2015 and Okuda 2010 foot-specific results above) strengthens
the case that foot-level force control is a genuine performance determinant, not an artefact of small
samples.

---

## 2. Centre of pressure trajectory within each foot (lead and trail separately)

### Systematic review — Sports Medicine 2026 (largest secondary source located)
Systematic review of ground reaction force and centre of pressure during the golf swing, *Sports
Medicine* (2026), PMID 41653371, PMCID PMC13198453 (open access, full text retrieved). **24
studies** met inclusion criteria out of 129 retrieved. This review supplied the full citation trail for
nearly every primary GRF/COP study referenced elsewhere in this document; see reference list at
the end of §2.

**Additional whole-foot pressure/GRF values surfaced by this review** (beyond what is captured
under the primary studies above):
- McHugh, O'Mahoney, Orishimo, Kremenic & Nicholas 2024 (*J Strength Cond Res* 38(3):599–606):
  lead-foot vertical GRF **139.5±19.6 %BW (professional)** vs **136.1±24.2 %BW (average
  golfers)** — a higher peak than the task's stated ~95% BW figure, from a different measurement
  definition/instant; lead-foot peak GRF correlated with ball speed at **R²=0.85**.
- Worsfold, Smith & Dyson 2007 (*J Sports Sci Med* 6(4):484–9): back-foot vertical GRF driver
  0.49 BW vs front(lead)-foot 0.84 BW; back-foot 3-iron/7-iron 0.82 BW vs front-foot 1.1 BW —
  **irons load both feet harder than the driver**, front foot always loaded higher than back foot at
  the measured instant.
- Bourgain, Sauret, Rouillon, Thoreux & Rouch 2017 (*Comput Methods Biomech Biomed Eng*
  20(sup1):29–30) and 2020 (*Proceedings* 49(1):45): horizontal GRF component correlates with
  the swing's global motor moment at **r=0.83**; combined vertical+horizontal GRF model
  R²=0.70 for motor-moment prediction.

### 24-study review's within-foot COP directional summary
The review states explicitly: **"CoP under the back foot shifts laterally, while the front foot CoP
moves anteriorly towards the forefoot"** across the swing — the clearest single-sentence
description located of within-foot COP direction, independent for each foot. It does not, however,
give numeric onset/offset timing or displacement magnitude for either foot separately, and states
that **ankle joint kinematics were not addressed by any of the 24 included studies**, and that
**foot musculature was not discussed by any of the 24 included studies** — direct confirmation
from the largest available secondary source that the literature gap named in this task's brief
(no foot musculature in the model) mirrors a gap in the primary literature itself, not a gap in
search effort.

Full reference trail extracted from this review for studies cited above and below:
- McHugh MP, O'Mahoney CA, Orishimo KF, Kremenic IJ, Nicholas SJ. Kinematic, kinetic, and
  temporal metrics associated with golf proficiency. *J Strength Cond Res*. 2024;38(3):599–606.
- Worsfold P, Smith NA, Dyson RJ. A comparison of golf shoe designs highlights greater ground
  reaction forces with shorter irons. *J Sports Sci Med*. 2007;6(4):484–9.
- Bourgain M, Sauret C, Rouillon O, Thoreux P, Rouch P. Contribution of vertical and horizontal
  components of ground reaction forces on global motor moment during a golf swing: a preliminary
  study. *Comput Methods Biomech Biomed Eng*. 2017;20(sup1):29–30.
- Bourgain M, Sauret C, Prum G, Valdes-Tamayo L, Rouillon O, Thoreux P, Rouch P. Effect of
  horizontal ground reaction forces during the golf swing: implications for technical solutions.
  *Proceedings*. 2020;49(1):45.
- Blenkinsop GM, Liang Y, Gallimore NJ, Hiley MJ. The effect of uphill and downhill slopes on
  weight transfer, alignment, and shot outcome in golf. *J Appl Biomech*. 2018;34(5):361–8.
- Jones KM, Wallace ES, Otto SR. Centre of pressure golf swing movement strategies are better
  defined using a continuous approach than by segregated styles. *J Sports Sci*. 2023;41(4):342–9.
- Jones KM, Wallace ES, Otto SR. The relationship between skill and ground reaction force
  variability in amateur golfers. *Sports Biomech*. 2021. DOI: 10.1080/14763141.2021.1965649.
- Jones KM, Wallace ES, Otto SR. Differences in the structure of variability in ground reaction
  force trajectories provide additional information about variability in the golf swing. *Proc Inst
  Mech Eng Part P J Sports Eng Technol*. 2018;232(4):375–84.
- Kim SE, Lee J, Lee SY, Lee H-D, Shim JK, Lee S-C. Small changes in ball position at address
  cause a chain effect in golf swing. *Sci Rep*. 2021;11(1):2694.
- Kim SE, Lee J, Lee SY, Lee H-D, Lee S-C, Shim JK. Golf swing in response to anteroposterior
  ball position. *Int J Sports Sci Coach*. 2023;18(5):1639–48.
- Kim SE, Koh Y-C, Cho J-H, Lee SY, Lee H-D, Lee S-C. Biomechanical effects of ball position on
  address position variables of elite golfers. *J Sports Sci Med*. 2018;17(4):589–98.
- Choi A, Sim T, Mun JH. Improved determination of dynamic balance using the centre of mass
  and centre of pressure inclination variables in a complete golf swing cycle. *J Sports Sci*.
  2016;34(10):906–14. (See §9 below — this is the strongest balance/CoP-CoM golf source found.)
- Ball KA, Best RJ. Different centre of pressure patterns within the golf stroke I: cluster analysis.
  *J Sports Sci*. 2007;25(7):757–70.
- Ball KA, Best RJ. Different centre of pressure patterns within the golf stroke II: group-based
  analysis. *J Sports Sci*. 2007;25(7):771–9.
- Ball KA, Best R. Golf styles and centre of pressure patterns when using different golf clubs.
  *J Sports Sci*. 2011;29(6):587–90.
- Ball K, Best R. Centre of pressure patterns in the golf swing: individual-based analysis. *Sports
  Biomech*. 2012;11(2):175–89.

### Slope and ball-position effects on within/between-foot COP (from the same review)
- Blenkinsop et al. 2018: on a downhill lie, COP sits **9.4% closer to the front(lead) foot**; on an
  uphill lie, COP sits **8.9% closer to the back(trail) foot** — quantifies how terrain forces
  redistribution of loading between feet, a demand that must be met by ankle/foot invertor-evertor
  and intrinsic musculature even though this review does not name the muscles involved.
- Kim et al. 2021 (ball position study): moving the ball backward in the stance shifted trail-foot
  COP by **−8.4±7.1 mm**.
- Jones et al. 2023: mediolateral COP variability explained R²=0.54 (driver) / R²=0.56 (5-iron) of
  swing-outcome variance; skilled golfers show lower COP-pattern variability across principal
  components (2 of 5 for driver, 4 of 5 for 5-iron) than less-skilled amateurs — variability itself,
  not just mean position, separates skill levels.

---

## 3. Intrinsic foot muscle EMG

**No golf-specific intrinsic foot muscle EMG study was found in any search.** This section states
that plainly per the task instruction. What follows is the best available EMG evidence from
comparable rotational/weight-shifting and balance tasks, which is the closest legitimate substitute.

### Lai, Cao, Wang, Zhong, Gong & Wang — intrinsic foot muscle recruitment under postural
perturbation (closest comparable-task EMG data found)
"Difference in the recruitment of intrinsic foot muscles ... under static and dynamic postural
conditions" (exact title as indexed), *PeerJ* (2023), PMID 37483972, PMCID PMC10362842 (open
access, full text retrieved). N=21 elderly participants (13 female, mean age 67±3 y; 8 male, mean
age 70±2 y) — **not golfers**, and an elderly rather than athletic sample, but the only source located
with quantified abductor hallucis (AbH) and flexor digitorum brevis (FDB) surface EMG during
graded postural challenge, which is mechanistically the same demand (resisting a shifting base of
support) the golf swing places on the feet.

**Static conditions — Sensory Organization Test (SOT), EMG normalised to unilateral-stance
reference, mean±SD**:
- AbH: SOT-1 (normal) 0.12±0.13; SOT-2 (eyes closed) 0.14±0.12; SOT-3 (moving visual
  surround) 0.14±0.13; SOT-4 (moving platform) 0.16±0.14; SOT-5 (vision+proprioception
  disturbed) 0.22±0.15; SOT-6 (vestibular+proprioception disturbed) **0.27±0.19** — a >2×
  increase in AbH activation from the easiest to the hardest static-balance condition.
- FDB: SOT-1 0.13±0.10; SOT-2 0.17±0.13; SOT-3 0.19±0.12; SOT-4 0.18±0.12; SOT-5
  0.34±0.16; SOT-6 **0.42±0.36** — FDB shows an even larger (>3×) relative increase than AbH
  under the hardest condition.
- Dynamic (Motor Control Test, platform translations): AbH activation increased significantly with
  translation speed (forward: F₂=64.34, p<0.001; backward: F₂=16.49, p<0.001); FDB likewise
  (backward: F₁.₃₇=25.01, p<0.001).

**Functional statements from the paper**: "Intrinsic foot muscles play a complementary role to
regulate postural stability when disturbances occur"; "the recruitment magnitude of intrinsic foot
muscles is positively correlated with the limit of stability"; intrinsic foot muscles "may contribute
to postural stability by increasing the limit of postural stability."

**Legitimate inference for golf**: the golf swing repeatedly and rapidly shifts the base-of-support
loading between feet (documented numerically in §1–2 above: VGRF swinging from ~25–35%BW
to ~90–113%BW at the lead foot within roughly one second, and from ~74–98%BW down to
~25–38%BW at the trail foot) while the trunk rotates and the arms/club add a large, asymmetric
inertial load well beyond anything in a standard balance-platform protocol. If AbH and FDB EMG
roughly doubles-to-triples between quiet stance and a moving-platform balance challenge in
non-athletes, it is reasonable to infer (not measure) that these same muscles are substantially
active during the swing's much larger and faster within-foot load transfer — but this is inference,
not golf-swing measurement, and the magnitude cannot be assumed to transfer quantitatively.

### Farris, Birch & Kelly 2020 — mechanistic role of plantar intrinsic muscles in foot stiffening
"Foot stiffening during the push-off phase of human walking is neither exclusively planar nor
fully explained by the windlass mechanism" (paraphrase of title as indexed), *J R Soc Interface*
17(168):20200208 (2020), PMID 32674708, PMCID PMC7423437 (open access). Not golf-specific
(walking push-off), but directly establishes general function: combined loading-frame and EMG
experiments showed that **active muscular contraction, not the passive windlass mechanism, is
the foot's primary source of rigidity for push-off** against the ground during bipedal walking; active
contractions of the ankle plantarflexors *and* the plantar intrinsic foot muscles both contribute
tension along the plantar aponeurosis. This overturns the classical passive-windlass-only teaching
and is directly relevant to any push-off/loading event in the golf swing (e.g. trail-foot late
downswing drive, lead-foot deceleration at/after impact), though again no golf data exists to
confirm the same mechanism operates in-swing.

### Short-foot / intrinsic foot muscle training — Lai et al. 2025 (companion trial, non-golf)
"Effects of intrinsic foot muscle training combined with lower extremity resistance training on
postural stability in older adults", *BMC Geriatrics* (2025), PMID 41023675, PMCID
PMC12482463. Authors: Lai Z, Cao M, Wang R, Zhong G, Gong P, Wang L. N=123 older adults,
randomised to short-foot+resistance training (SF-RT), towel-curl+resistance training (TC-RT),
resistance-training-only, or control, 3×/week for 8 weeks. SF-RT produced "significant
improvement at equilibrium, strategy and overall scores" beyond the other groups, and "additional
short-foot training militated extra effect on improving static postural stability, mobility, foot
muscle strength and morphology." Confirms intrinsic foot muscle training is a trainable variable
that measurably changes balance outcomes — again general population, not golf, but relevant to
any recommendation to golfers about foot-specific training.

**Muscle-spindle sensory context** (not EMG but directly relevant to the intrinsic-muscle
question): "Firing properties of muscle spindle afferents in the intrinsic foot muscles and tactile
afferents from the sole during upright stance," *Exp Physiol* (2025), PMID 40211475, PMCID
PMC12486321. Microneurographic recordings found spindle-afferent firing rates in intrinsic foot
muscles correlated with centre-of-pressure changes, "primarily along the anteroposterior axis," in
**67% of endings** recorded during unsupported standing — evidence that intrinsic foot muscles are
not just force generators but part of a closed-loop proprioceptive sensing system for whole-body
sway, again in a non-golf, non-athletic sample.

**Verdict for the model**: no golf-specific intrinsic foot muscle EMG exists anywhere in the
literature located. The comparable-task evidence (postural perturbation, walking push-off, foot
proprioception) is real, quantified, and mechanistically transferable in principle, but every number
above must be flagged in the model as **cross-task inference, not golf measurement**, if used.

---

## 4. Tibialis posterior, flexor hallucis longus, flexor digitorum longus — deep calf compartment

**No golf-specific EMG for tibialis posterior (TP), flexor hallucis longus (FHL), or flexor digitorum
longus (FDL) was found in any search route tried** (EuropePMC keyword search, PubMed HTML
search). This is stated plainly per the task instruction. General, non-golf function with sources:

- **Tibialis posterior**: primary dynamic supporter of the medial longitudinal arch and the main
  active decelerator/controller of subtalar pronation in gait — well-established orthopaedic/
  biomechanics consensus; the search above surfaced only tangential EMG comparators (e.g. a 2025
  *Frontiers in Pediatrics* flatfoot-surgery study, PMID 41341107, PMCID PMC12668922, which
  measured tibialis **anterior**, peroneus longus and medial gastrocnemius — not TP — around
  subtalar arthroereisis, finding peroneus longus peak activation **increased** and tibialis anterior /
  medial gastrocnemius peak activation **decreased** post-operatively; included here only because it
  was the closest EMG hit, not because it answers the TP question). No study located isolates TP
  EMG amplitude or timing in gait, running, or any rotational sport task via the search routes used.
- **Flexor hallucis longus**: established function is plantarflexion of the hallux and a secondary
  ankle plantarflexor, classically implicated in late-stance/push-off hallux loading and windlass
  engagement. Farris, Birch & Kelly 2020 (§3 above, PMID 32674708) supports an active (not
  purely passive-tendon) role for the deep posterior compartment plantarflexors as a group during
  push-off, but does not isolate FHL from the other plantarflexors by name in the reported EMG.
  No FHL-specific EMG timing/amplitude data (golf or otherwise) was retrieved.
- **Flexor digitorum longus**: no EMG data (golf or comparable task) was retrieved via any search
  route. Established anatomical function (toe flexion, ankle plantarflexion assistance, dynamic arch
  support) is textbook knowledge, not further sourced here since no primary EMG evidence at all
  was located to attach it to.

**This is a genuine, stated evidence gap** — not a search-effort failure. The Sports Medicine 2026
systematic review (§2, PMC13198453) independently confirms that **none of its 24 included
GRF/COP golf studies discussed foot musculature at all**, consistent with zero hits for TP/FHL/FDL
EMG across every search route attempted here.

---

## 5. Peroneus brevis vs peroneus longus

**No study was found that separates peroneus brevis from peroneus longus EMG in golf.** Existing
project data (per the task's framing) already covers peroneus longus only; the searches run here
(EuropePMC keyword search for "peroneus brevis longus EMG golf swing lateral ankle") returned
**zero golf-relevant hits** — nine results, all Journal of Athletic Training conference supplements or
AOFAS meeting abstracts with no retrievable abstract text, none golf-specific. The one indirectly
relevant hit from a related search (§4, PMID 41341107, flatfoot-surgery EMG) measured peroneus
**longus** only, again not brevis, and not in golf. No brevis-specific golf or comparable-task EMG
data could be located by any route attempted. This must be recorded as an open gap: if the model
currently carries a peroneus longus curve inferred or measured from any source, there is **no
evidence base located anywhere** to derive an independent peroneus brevis curve — at most, brevis
could be modelled as covarying with longus (both are evertors, both cross the lateral ankle, both
resist inversion) but this would be an assumption, not a sourced finding.

---

## 6. Popliteus

**No golf-specific popliteus data exists** (expected — popliteus is rarely instrumented even in
gait-EMG studies due to its small size and deep location). General anatomical/functional sources:

- Nyland, Lachman, Kocabey, Brosky, Altun & Caborn 2005, "Anatomy, function, and rehabilitation
  of the popliteus musculotendinous complex," *J Orthop Sports Phys Ther* (2005), PMID 15839310.
  Popliteus functions to **"unlock and internally rotate the knee joint (tibia) during flexion
  initiation"** and acts as "a dynamic guidance system for monitoring and controlling subtle
  transverse- and frontal-plane knee joint movements"; also assists posterolateral knee stability
  during stance and controls anteroposterior lateral-meniscus movement.
- Kim, Sung, Yu et al. (uncertain author order from search excerpt), "Principles and mechanisms of
  automatic rotation during terminal extension in the human knee joint," *J Anat* (1992), PMID
  1506284: popliteus reverses the knee's automatic (screw-home) rotation **"during initial
  flexion,"** working against the passive ACL/PCL/condyle-curvature-driven locking mechanism
  described in this classic paper.
- "Locking at the knee joint," *J Anat* (1953), PMID 13044721 — foundational anatomical
  description of terminal-extension locking and the flexion-initiation unlocking role popliteus plays
  against it; pre-dates modern EMG and so contains no activation values, only anatomical/mechanical
  reasoning.
- "Popliteus Tendon Morphology: Anatomical Classification and Clinical Implications," *Biomedicines*
  (2025), PMID 41007617, PMCID PMC12467253: modern review confirming the popliteus tendon
  "contributes significantly to knee rotational control and meniscal stabilization, particularly in
  athletic populations," with a role in posterolateral-corner stability and rotational-instability
  management.
- "Layer-Specific Architecture and Nerve Innervation of the Popliteus Muscle," *Diagnostics* (2026),
  PMID 41897567, PMCID PMC13024952: recent anatomical study finding popliteus "functions as a
  dual motor unit rather than a uniform structure," with separately innervated superficial and deep
  layers providing compartmentalised control of knee stability and tibial rotation — a mechanistic
  basis for fine-grained rotational control, but again no EMG amplitude/timing data, golf or
  otherwise.

**Relevance to golf inferred (not measured)**: the lead knee undergoes rapid internal rotation
during the downswing as the pelvis and femur rotate over a planted, relatively fixed tibia/foot —
mechanically exactly the "unlock and internally rotate the tibia during flexion" role described for
popliteus above, compounded by the femur externally rotating relative to a foot that is itself
resisting the ~17–19 Nm free-moment torque named in this task's brief. No golf study has measured
popliteus EMG or activation to confirm this, but the joint mechanics described in Nyland 2005 and
the 1992/1953 sources align directionally with what the lead knee must be doing kinematically
during the downswing (documented already in `03-lower-limb-and-hip-activation.md` and
`12-functional-anatomy-and-moment-arms.md` for the surrounding hip/knee musculature).

---

## 7. Footwear and traction

This is the best-populated section in this document after plantar pressure itself — two dedicated
golf-shoe biomechanics papers were located and fully retrieved, both from the same research group
(University of Ulster) using the same 24-golfer test panel across driver/iron conditions.

### Worsfold, Smith & Dyson 2008 — shoe-turf torque by handicap level and shoe type
"[Golf shoe torque paper]" — best available reconstructed title/citation: Worsfold P et al.,
*J Sports Sci Med* (2008), PMID 24149910, PMCID PMC3761900 (open access, full text retrieved).
N=24 golfers, 8 per handicap tier (low/medium/high), driver shots, three shoe conditions (metal
spike, alternative/soft spike, flat sole).

**Back(trail)-foot torque, driver, Nm mean(SD), by handicap × shoe**:
- Low handicap: metal spike **18.2(3.1)**, alternative **15.8(3.7)**, flat sole **14.4(2.4)**.
- Medium handicap: metal spike 15.5(4.7), alternative 13.2(3.1), flat sole 11.6(4.0).
- High handicap: metal spike 14.2(7.4), alternative 11.0(4.4), flat sole 11.9(5.6).
- Low-handicap back-foot driver torque significantly exceeds medium/high handicap (p<0.05) —
  **more skilled golfers generate more resistive/propulsive torque at the trail foot**, and metal
  spikes consistently permit the highest torque of the three shoe conditions within every handicap
  tier.

**Front(lead)-foot torque, driver, Nm mean(SD)**: low handicap metal spike 42.1(11.0), alternative
42.4(8.3), flat sole 38.9(8.5); medium/high handicap range 40.0(8.4)–43.5(5.9) — **front-foot
torque is roughly 2.5–3× back-foot torque** and shows comparatively little sensitivity to shoe type
or handicap, i.e. the lead foot's rotational resistance demand is large and fairly constant across
skill levels, while the trail foot's is smaller but more skill/shoe-dependent.

**Peak and range torque summary figures also reported**: maximum torque (Tzmax) back foot
**6–7 Nm** vs front foot **17–19 Nm**; total generated torque range back foot 10–16 Nm vs front
foot ~40 Nm. **The front-foot Tzmax figure of 17–19 Nm matches, almost exactly, the task's stated
lead-foot free-moment of 17–19 Nm** — strong independent corroboration that the free-moment
figure in the task brief is a real, correctly-scaled measurement, and that it is concentrated
overwhelmingly at the lead foot rather than distributed evenly between feet.

### Companion paper — kinetic assessment of outer-sole design, regional pressure detail
Companion paper (same group/panel), *J Sports Sci Med* (2009), PMID 24149603, PMCID
PMC3761538 (open access, full text retrieved). N=18 right-handed golfers, handicap 0–19 (mean
12.4±7.8), age 29.0±2.1 y, height 1.80±0.02 m, mass 81.3±2.7 kg. Plantar pressure at 500 Hz, GRF
at 1000 Hz, video at 200 Hz; three shoe conditions as above.

**Back-foot torque (Nm)**: Tzmax metal spike 7.8(1.6), alternative 7.2(1.6), flat sole 7.2(1.5); Tz
range metal spike **14.8(1.8)**, alternative 14.3(1.9), flat sole **13.2(2.0)** (metal spike vs flat sole
p<0.05 for range).

**Front-foot torque (Nm)**: Tzmax metal spike 20.8(3.7), alternative 20.4(4.3), flat sole 19.7(4.0);
Tz range metal spike 38.1(5.9), alternative 38.9(5.5), flat sole 39.2(4.2) — no significant shoe
effect at the front foot in this cohort (contrasts mildly with the torque-by-handicap paper above,
likely reflecting the mixed-handicap vs handicap-stratified sampling difference between the two
papers).

**Regional peak plantar pressure (kPa) by shoe type, front foot**: R5 lateral midfoot — metal
spike **115.3**, alternative spike **87.6**, flat sole **102.3** (all pairwise p<0.05); R2 posterior
medial heel — metal spike 36.2, alternative 33.0, flat sole 27.4 (p<0.05); R4 anterior medial heel —
metal spike 19.4, alternative 17.0, flat sole 13.4 (p<0.05). **Metal spikes concentrate pressure at
the lateral midfoot and heel far more than flat soles** — mechanically consistent with spikes
providing a fixed rotational anchor point that flat soles cannot, forcing more of the lead-foot
rotational resistance through those specific regions rather than distributing it.

**Regional peak plantar pressure (kPa) by shoe type, back foot**: R6 medial midfoot — metal spike
67.8, alternative 56.3, flat sole 67.1 (p<0.05); R3 anterior lateral heel — metal spike 16.4,
alternative 13.9, flat sole 12.2 (p<0.05); R8 mid-forefoot — metal spike 70.5, alternative **77.5**,
flat sole 66.1 (p<0.05, alternative-spike highest here, the one region where soft spikes exceed
metal).

**Friction and vertical force**: coefficient of friction (COFxy) 0.607–0.654 across all three shoe
types at both feet, **no significant difference by shoe type** (p>0.05); maximal vertical force
(Fzmax) also **not significantly different by shoe type** at either foot (p>0.05). This is an important
qualifier: shoe/spike design changes *where* and *how much rotational torque* is generated and
*where* pressure concentrates, but does **not** change the total vertical load or the coefficient of
friction at the shoe-turf interface in this dataset — the mechanical effect of spikes is specifically
rotational/torsional, not vertical-load-bearing.

**Synthesis for the model**: footwear/traction studies are the clearest quantitative bridge in the
entire literature between the task's free-moment torque figure (17–19 Nm) and a plausible
mechanism — metal spikes measurably increase the torque the shoe-ground interface can resist/
transmit relative to flat soles, and this is concentrated at specific foot regions (lateral midfoot,
heel) rather than uniform. None of this is EMG — it is externally-measured torque and pressure —
but it directly supports the inference (see final summary) that intrinsic and extrinsic foot/ankle
musculature must actively resist this torque internally, since the shoe-ground interface only
provides the *external* friction/spike anchoring, not the internal muscular counter-torque itself.

---

## 8. Barefoot vs shod, and foot function / arch behaviour / balance training in golfers

**No dedicated barefoot-vs-shod golf swing study was found.** Direct EuropePMC and PubMed
searches ("golf barefoot shoe driving distance balance", "barefoot shod golf swing foot") returned
**zero golf-relevant results** on both routes. The only barefoot-related data point anywhere in this
document is second-hand, embedded in the Pataky 2015 paper's discussion (§1 above): Healy 2009
(MSc thesis, Dublin City University, unretrieved directly) tested barefoot and found **no COPx
difference** between <3 and 10–18 handicap golfers, which Pataky et al. explicitly attribute to
barefoot testing "likely involving both reduced foot stability and reduced foot-ground friction with
respect to shod testing" — i.e. the one barefoot golf data point available suggests barefoot testing
*erases* a skill-related COP signal that is present when golfers are shod, implying the shoe/spike
interface (§7) is doing biomechanical work that bare skin-to-turf contact cannot replicate. This is a
single, indirect, thesis-sourced data point — not a peer-reviewed dedicated study — and should be
weighted accordingly.

**Foot function / arch behaviour in golfers, non-barefoot-specific**: the Ozturk 2019 study (§1
above, PMC6506813) is the only source with direct arch-relevant static/dynamic pressure data in
golfers (forefoot/rearfoot load ratios, foot angle), though it does not test barefoot vs shod
conditions — all measurements were presumably in athletic footwear (not stated explicitly in the
retrieved text). No golf study measuring arch height, arch index, or navicular drop was located.

**Balance training in golfers** (see also §9 for balance *measurement*): Li, Ruan & Zhang 2024,
"Impact of Four Weeks of TOGU Training on Neuromuscular Control and Golf Swing Performance,"
*J Funct Morphol Kinesiol* (2024), PMID 39584896, PMCID PMC11587031 (open access, full text
retrieved) — this is an intervention trial, not barefoot-specific, but it is the strongest evidence in
this whole document that foot/ankle/balance training transfers to golf performance. N=29
right-handed men (TOGU balance-equipment training group n=16, control n=13), age 21.06±1.06 y,
height 175.19±5.14 cm, weight 72.11±10.04 kg, handicap 15–20. Protocol: 4 weeks, 3×/week,
60 min sessions (10 min warm-up/cool-down each side).

**Balance outcome changes (mCTSIB, modified Clinical Test of Sensory Integration on Balance)**:
sway reduced foam-eyes-open **−30.9%** (p<0.01), firm-eyes-closed **−35.18%** (p<0.05),
foam-eyes-closed **−36.78%** (p<0.001). **Unilateral stance test (UST)**: left-eyes-open
**−34.39%** (p<0.001), left-eyes-closed −29.92% (p<0.001), right-eyes-open −48.67% (p<0.01),
right-eyes-closed −39.38% (p=0.0857, n.s.).

**Golf performance changes after 4 weeks of balance training**: clubhead speed **+5.73%**
(p<0.01); ball speed **+11.3%** (p<0.001); driving distance +6.67% (p=0.0553, borderline n.s.);
hitting efficiency +5.45% (p<0.01); total Functional Movement Screen (FMS) score +11.48%; deep
squat sub-score +23.07%.

**Significance for the model**: this is the single best piece of evidence located anywhere in this
research task that foot/ankle/balance-system training has a *causal*, *measured*, *golf-specific*
performance effect — sway and single-leg balance improved substantially, and clubhead/ball speed
improved significantly in the same golfers over the same 4 weeks. It does not isolate which
muscles produced the balance improvement (TOGU equipment training is a whole-kinetic-chain
proprioceptive stimulus, not an isolated foot exercise), so it cannot be used to attribute the
performance gain to intrinsic foot muscles specifically — but it is strong indirect support that the
foot/ankle/balance system as a whole is a genuine, trainable performance lever in golf, closing the
loop back to the task's opening premise that this musculature "must" be doing something
functionally important.

---

## 9. Balance and postural control in golfers

### Choi, Sim & Mun 2016 — the primary golf-specific balance/COP-COM source
"Improved determination of dynamic balance using the centre of mass and centre of pressure
inclination variables in a complete golf swing cycle," *J Sports Sci* 34(10):906–14 (2016) — cited
via the Sports Medicine 2026 systematic review (§2, PMC13198453; not independently retrieved in
full text, so figures below come from the review's summary, not the primary paper directly).
**CoP-to-CoM inclination angle differed by 6.13±2.4° between skilled and novice golfers** during
downswing — the review frames this as the clearest quantified skill-level balance/dynamic-stability
marker in the golf literature. This is a whole-body dynamic-balance metric (CoP relative to CoM),
not a foot-region or muscle-level metric, but it is golf-specific and skill-differentiating.

### Li, Ruan & Zhang 2024 (TOGU training study) — see full detail in §8
Repeated here for completeness of this section: static and dynamic balance (mCTSIB sway,
unilateral stance test) improved 30–49% across most conditions after 4 weeks of balance training,
alongside significant clubhead-speed (+5.73%) and ball-speed (+11.3%) gains in the same cohort
(N=29, handicap 15–20). This is the only located study directly correlating a *balance
intervention* with golf performance change, as distinct from a cross-sectional skill-correlation
study.

### Functional movement screening — collegiate golfers
"Using a Golf Specific Functional Movement Screen to Predict Golf Performance in Collegiate
Golfers," *PeerJ* (2024), PMID 38803584, PMCID PMC11129693 (abstract-level detail only
retrieved). Cross-sectional study finding "pelvic rotation and lower-body rotation abilities"
predicted golf skill performance in collegiate golfers — supports lower-body/rotational control as a
performance determinant but does not isolate ankle/foot balance specifically, and no numeric
correlation coefficients were retrieved from the available excerpt.

### What could not be found for this section
No study was located that: (a) directly correlates single-leg static balance test scores (e.g. Y-Balance,
single-leg stance time, Star Excursion) with handicap or clubhead speed in golfers as a
cross-sectional predictor variable — the closest analogue is the Choi 2016 dynamic CoP-CoM
metric (skill-group comparison, not a continuous correlation) and the Li 2024 training-effect study
(intervention, not baseline correlation); (b) measures ankle strategy vs hip strategy balance
responses specifically in golfers; (c) reports a golf-specific normative single-leg balance database.
This is recorded as an explicit gap — searches used multiple keyword combinations ("golfer
postural sway balance single leg handicap clubhead speed", "golf balance stability training
performance clubhead") and returned no further golf-specific cross-sectional balance-correlation
studies beyond the two above.

---

## 10. Ankle joint kinematics through the swing

This section improved substantially over the course of the search — three golf-specific sources
with actual ankle-angle numbers were eventually located, correcting an initial round of searches
that returned zero golf-specific ankle-kinematics hits.

### Lin, Peng, Yang, Hsu, Hamill & Tang 2023 — lead-ankle 3D kinematics during the downswing
"Lower Limb Biomechanics during the Golf Downswing in Individuals with and without a History of
Knee Joint Injury," *Bioengineering (Basel)* 10(5):626 (2023), PMID 37237695, PMCID
PMC10215287 (open access, full text retrieved). N=20 professional golfers (10 with prior knee
injury [KIH+], 10 without [KIH−]), 3D motion capture, **lead ankle only**, downswing phase.

**Ankle abduction/adduction (lead leg, downswing)**: KIH+ ankle abduction **10.48±3.64°** vs
KIH− **15.21±3.12°** (t=−3.11, p=0.006); adduction/abduction ROM KIH+ **9.01±3.16°** vs KIH−
**5.61±2.07°** (t=2.84, p=0.011; effect sizes 1.3 and 1.2 respectively) — golfers with a knee injury
history use **less peak ankle abduction but a larger ab/adduction excursion range**, consistent with
the paper's framing that prior-injury golfers "adjust hip and ankle joint angles to minimize impact"
on the previously injured knee.

**Ankle plantarflexion/dorsiflexion (lead leg, downswing)**: KIH+ plantarflexion 20.59±5.00°,
dorsiflexion −3.28±9.54°, ROM 23.87±6.44°; KIH− plantarflexion 17.96±2.96°, dorsiflexion
−4.52±6.26°, ROM 22.48±5.38° — **no significant group difference** (p>0.05) in the sagittal
plane. Internal/external ankle rotation: no significant group difference either (p>00.05, both
groups). No ankle kinetic (moment/torque) data was reported in this paper — kinematics only.

### Quinn, Olivier & McKinon 2022 — lead ankle dorsiflexion as a low-back-pain risk marker
"Lower Quadrant Swing Biomechanics Identifies Golfers With Increased Risk of Low Back Pain: A
Prospective Longitudinal Cohort Study," *J Sport Rehabil* (2022), PMID 35894899. N=41
injury-free golfers at baseline, 10 drives each, 3D lower-quadrant kinematics recorded; 6-month
prospective follow-up, 17 (41%) developed low back pain (LBP).

**Baseline kinematic differences, LBP-group vs uninjured-group (all baseline, all golfers
injury-free at time of measurement)**:
- **Lead ankle dorsiflexion at setup/address: 4° less in the eventual-LBP group** (p=0.01, effect
  size 0.82).
- **Lead ankle dorsiflexion at top of backswing: 6° less in the eventual-LBP group** (p=0.01,
  effect size 0.82).
- Lead knee flexion at top of backswing: 6° less in the eventual-LBP group (p=0.05, ES=0.64).
- Trail hip adduction at top of backswing: 6° more in the eventual-LBP group (p=0.02, ES=0.79).
- Trail knee flexion at impact: 9° more in the eventual-LBP group (p=0.05, ES=−0.64).
- Trail hip adduction at end of follow-through: 6° more in the eventual-LBP group (p<0.001,
  ES=1.00).

This is the **only source located that treats ankle dorsiflexion as a quantified, clinically predictive
variable in golf** — reduced lead-ankle dorsiflexion at two distinct phases (setup and top-of-
backswing) preceded low back pain onset by up to 6 months, ahead of any pain being present. The
authors frame this as a possible proximal-compensation chain: restricted ankle dorsiflexion range
may force compensatory motion up the kinetic chain into the knee, hip and eventually lumbar
spine. No causal mechanism is proven (this is an associative cohort study), but the ankle variable
is measured with real degree values and real statistical power (N=41, effect sizes 0.64–1.00).

### Rogers, Strike & Wallace 2004 — natural-experiment evidence for ankle-joint-complex (AJC)
importance, from trans-tibial amputees
"The effect of prosthetic torsional stiffness on the golf swing kinematics of a left and a right-sided
trans-tibial amputee," *Prosthet Orthot Int* (2004), PMID 15382806. N=2 (one right-sided, one
left-sided trans-tibial amputee), 3-wood shots, three prosthetic torsion-device conditions (two
stiffness settings, one with no torsion device), 3D video analysis at address, top-of-backswing, and
end-of-follow-through.

**Key finding, verbatim**: "The golf swing is a biomechanically complex movement requiring
three-dimensional movements at the ankle joint complex (AJC), the hips and shoulders." Adding a
torsion device (restoring some transverse-plane AJC mobility to the prosthesis) **improved hip and
shoulder rotation in the left-sided (lead-leg) amputee** without increasing perceived stump stress,
but had **minimal effect on hip/shoulder rotation in the right-sided (trail-leg) amputee** — instead,
"the main problem faced by the right-side amputee was **a loss of the sagittal-plane movement of
ankle joint plantarflexion at [end of follow-through]**, rather than the transverse-plane movement."
In other words: the **lead ankle's critical degree of freedom is transverse-plane (rotational)**,
while the **trail ankle's critical degree of freedom is sagittal-plane plantarflexion** (consistent with
the trail foot's classic late-downswing/follow-through "roll-up onto the toe" push-off role) — a
clean natural-experiment dissociation between the two ankles' functional demands that no
able-bodied EMG or kinematic study located in this search stated as explicitly.

### Sidiropoulos, Nelson, Pruziner, Glasberg & Maikos 2023 — lower-limb-loss veterans, weight
shift and X-factor by amputation side/level
"Evaluation of Weight Shift and X-Factor During Golf Swing of Veterans With Lower Limb Loss,"
*Am J Phys Med Rehabil* 102(1):85–91 (2023), PMID 34864764, PMCID PMC9163200 (open
access, full text retrieved). Compares trail-limb amputation (TLA) vs lead-limb amputation (LLA),
and below-knee amputation (BKA) vs above-knee amputation (AKA), against able-bodied normative
weight-shift values.

**Able-bodied normative lead/trail weight-shift percentages by phase** (control reference values
reported in this paper — useful independent of the amputee comparison): address **50%/50%**;
transition **20% lead / 80% trail**; impact **80% lead / 20% trail**; follow-through **70% lead /
30% trail**.

**Weight-shift %, TLA vs LLA**: impact — lead limb TLA 91.0(25.5) vs LLA 43.0(13.0); trail limb
TLA 9.0(25.5) vs LLA 57.0(13.0). Follow-through — lead limb TLA 79.5(12.5) vs LLA 38.0(51.0);
trail limb TLA 20.5(12.5) vs LLA 62.0(51.0). **TLA golfers (intact lead leg/foot) achieve
near-normal or exaggerated lead-foot loading at impact (91%, vs the 80% able-bodied norm);
LLA golfers (impaired lead leg/foot) fall well short of normal lead-foot loading (43% vs 80%
norm)** — direct evidence that an intact, fully-functional lead foot/ankle is necessary to hit the
normal impact weight-shift target, and that losing it cannot be fully compensated by the rest of the
kinetic chain.

**Weight-shift %, BKA vs AKA (transition phase)**: lead limb BKA 20.0(16.75) vs AKA 60.0(37.0);
trail limb BKA 80.0(16.75) vs AKA 40.0(37.0). BKA (below-knee, i.e. foot/ankle replaced by
prosthesis but native knee retained) golfers match the able-bodied transition norm (20% lead/80%
trail) almost exactly, while AKA (above-knee, native ankle **and** knee both lost) golfers deviate far
more (60% lead/40% trail) — suggesting that **losing the native knee in addition to the foot/ankle
causes substantially more disruption to normal weight-shift timing than losing the foot/ankle
alone**, an indirect but real signal about the relative contribution of the knee vs the foot/ankle to
weight-shift control (though it cannot isolate the foot/ankle's contribution in isolation from the
knee's, since BKA golfers still lack a native ankle too).

**X-factor (pelvis-thorax separation), degrees, LLA vs TLA**: pelvis LLA −34.0(11.5) vs TLA
−28.5(15.5); thorax LLA −34.0(11.5) vs TLA −28.5(15.75); maximum LLA −35.0(12.5) vs TLA
−29.0(14.5). Able-bodied normative range: pelvis −37 to −51°, thorax −39 to −52°, maximum −39
to −53°. **Both amputee groups fall short of the able-bodied X-factor range**, but LLA (lead-limb
loss) golfers retain a numerically larger X-factor than TLA (trail-limb loss) golfers — i.e. losing the
trail leg/foot costs more rotational separation than losing the lead leg/foot, the opposite pattern
from the weight-shift finding above, where lead-limb loss was more disruptive. This asymmetry
(trail limb more important for X-factor generation, lead limb more important for impact
weight-shift magnitude) is a genuine, quantified, if indirect, functional dissociation between the
two feet/ankles' roles.

---

## Synthesis: measured vs inferred, and what this means for the muscle model

**Directly measured in golf, with real numbers (safe to encode as data)**: whole-foot and
regional plantar pressure (§1); lead/trail vertical GRF by phase (§1, §2); shoe-turf torque by shoe
type and handicap, matching the task's 17–19 Nm lead-foot free-moment almost exactly (§7);
regional plantar pressure by shoe type (§7); whole-body CoP-CoM inclination angle skill
differences (§9); balance-training-induced sway and clubhead-speed changes (§8/§9); lead-ankle
sagittal-plane angles at setup/top-of-backswing and their prospective association with low back
pain (§10); lead-ankle frontal-plane (abduction/adduction) angles during the downswing, split by
knee-injury history (§10); amputee/prosthetic natural-experiment kinematics establishing that the
lead ankle's critical role is transverse-plane (rotational) and the trail ankle's is sagittal-plane
(plantarflexion at follow-through) (§10).

**Not measured in golf anywhere, by any muscle or joint named in the task (genuine literature
gaps, confirmed by both targeted search and the independent 24-study systematic review's
explicit statement that none of its studies discussed foot musculature or ankle kinematics)**:
intrinsic foot muscle EMG (abductor hallucis, flexor digitorum brevis, quadratus plantae) — zero
golf studies (§3); tibialis posterior, flexor hallucis longus, flexor digitorum longus EMG — zero
golf studies, and no isolated non-golf EMG for TP or FDL specifically either (§4); peroneus brevis
vs longus separation — zero golf studies, zero comparable-task studies located that separate them
(§5); popliteus EMG or activation — zero golf studies, and essentially no EMG anywhere in the
popliteus literature located, golf or otherwise, only anatomical/mechanical reasoning (§6); barefoot
vs shod golf swing comparison — zero dedicated studies, one indirect thesis-sourced data point
only (§8).

**What can legitimately be inferred, and what cannot**: the plantar-pressure, GRF, and
shoe-torque data (§1, §2, §7) establish *that* large, phase-varying, laterally-asymmetric forces and
torques pass through specific foot regions at specific times, and that this is tightly coupled to skill
level and clubhead speed. Mechanically, some combination of extrinsic and intrinsic foot/ankle
musculature *must* generate, resist, or transmit these forces — there is no alternative structure
that could do so (the passive skeleton and ligaments alone cannot generate the active,
skill-differentiated torque increases documented in §7, and Farris et al. 2020, §3, specifically
showed that even the passive windlass mechanism is insufficient to explain foot rigidity during a
much simpler task, walking push-off). It is legitimate to infer that intrinsic foot muscles, tibialis
posterior, FHL, FDL, peroneus brevis, and popliteus are *active* during the golf swing and that
their activation almost certainly scales with the documented pressure/torque demands. It is **not**
legitimate to infer specific %MVC magnitudes, timing curves, or phase-by-phase activation tables
for any of these muscles from pressure/torque/kinematic data alone — force plates and pressure
insoles measure the net external consequence of muscle action combined with passive tissue and
inertial effects, not muscle activation itself, and no golf EMG study of these muscles exists to
calibrate that inference. Any activation curve the model assigns to these muscles based on this
document would be a modelled hypothesis, not a sourced measurement, and must be labelled as
such if used.

**Top 3 gaps, restated for emphasis**: (1) zero EMG of any kind — golf or comparable-task — for
tibialis posterior, flexor hallucis longus, flexor digitorum longus, or popliteus; (2) zero
golf-specific EMG for any intrinsic foot muscle, with only elderly non-athletic postural-perturbation
data as a distant proxy; (3) zero study anywhere that separates peroneus brevis from peroneus
longus in any rotational, weight-shifting, or golf task.






