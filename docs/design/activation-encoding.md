# Visual Encoding for Muscle Activation Intensity on a Transparent 3D Figure

Status: IN PROGRESS (research log — building incrementally)
Scope: evaluate owner's proposal ("opacity alone = intensity") against perception/rendering literature; recommend final encoding.

## Design context (fixed)
- Transparent wireframe/mannequin figure; muscle zones drawn as thin outlines; fill colour appears only where a muscle is active.
- ~240 rendered zones (~120 muscle groups x 2 sides), heavy depth overlap along view rays (see-through body).
- Figure rotates freely, animates through golf swing (real-time 3D).
- ~2/3 of zones have no data -> need quiet, discoverable "never measured" state.
- Need a distinct "uncertain/provisional" state.

---

## Source log

(Each entry: claim/finding -> numeric detail if any -> source citation -> URL/access method.)

### S1 — Cleveland & McGill (1984) elementary perceptual tasks, ranked most->least accurate
1. Position along a common (aligned) scale
2. Position along non-aligned scales
3. Length / direction / angle (grouped, roughly tied)
4. Area
5. Volume, curvature
6. Shading / colour saturation — LEAST accurate
Basis: psychophysical judgement experiments; theoretically grounded in Stevens' Power Law — length has exponent ~1 (accurate), area <1 (systematic underestimation), volume much lower (severe underestimation). Replicated by Heer & Bostock (2010, crowdsourced) with same ordering.
Source: Cleveland & McGill 1984, "Graphical Perception: Theory, Experimentation, and Application" (JASA); secondary summary via textbookofusability.com/glossary/cleveland-mcgill-hierarchy.html and vizdata.org STA313 slides (Duke).
Note: opacity/transparency/alpha is NOT part of the original 1984 task set at all — it predates alpha-blended computer graphics as a common encoding.

### S2 — Munzner (Visualization Analysis & Design, 2014) channel effectiveness ranking
Magnitude channels (ordered attributes), most -> least effective:
1. Position on common scale
2. Position on unaligned scale
3. Length (1D size)
4. Tilt/angle
5. Area (2D size)
6. Depth (3D position)
7. Color luminance
8. Color saturation
9. Curvature
10. Volume (3D size)

Identity channels (categorical, not for magnitude): Spatial region, Color hue, Motion, Shape.
Source: T. Munzner, UBC CS547 course slides "Marks and Channels" (cs.ubc.ca/~tmm/courses/547-20/slides/marks.pdf — PDF text-extraction failed via WebFetch, confirmed instead via SlideShare mirror of her Lecture 2 deck, "Channels: Expressiveness types and effectiveness rankings").
**Key finding: opacity/transparency does not appear anywhere in Munzner's canonical magnitude- or identity-channel list.** It is absent from the taxonomy used as the field's standard reference for channel effectiveness — i.e. it has not been empirically validated/ranked as a magnitude channel in the primary perceptual-ranking literature at all. This is itself evidence against treating opacity as a first-class quantitative channel: the visualization community's own effectiveness ranking has no slot for it.

