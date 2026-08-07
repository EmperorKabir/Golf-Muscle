# Model visual specification (T-014)

Established from three reference images supplied by the user on 2026-08-07, plus explicit rejections of four
earlier style studies. This supersedes the loose description in D-002.

## Reference images

Held in `docs/design/reference/`:

| File | What it demonstrates | User's verdict |
|---|---|---|
| `target-mesh-front-back.png` | 3D polygonal mesh, front and back. Correct human proportion, full anatomical coverage, real muscle relief | Target for **form and coverage**. The polygon topology grid — "the random squared lines" — is explicitly **not** wanted |
| `target-zone-linework.png` | 2D line-art anatomical figure. Every muscle group outlined, whole body covered, clean single-weight lines, no gaps | "not bad example but would need to be 3d obviously" — target for the **zone line treatment** |
| `target-sculpted-form.png` | Sculpted 3D body, muscle relief expressed through surface form and shading rather than outlines | "also not bad" — target for **3D form quality** |

## The specification, resolved

**A properly sculpted 3D human body, of the anatomical quality of `target-sculpted-form.png`, with muscle
zone boundaries drawn as clean single-weight outlines in the manner of `target-zone-linework.png`, and with
no polygon topology visible.**

The body is transparent (D-002), so zones on the far side are visible through the near side. Colour fill
appears only where a muscle is working.

## Binding requirements from the user's critique of the first studies

1. **Full anatomical coverage. No bare areas.** Every region of the body surface belongs to a named muscle
   zone. A gap implies "no muscle exists here", which is false and misleading. This was the single biggest
   failure of the first studies.
2. **Correct anatomical extents.** The user's example: the quadriceps must occupy the actual quadriceps
   region — the full front and side of the thigh from hip to knee — not a narrow strip. Every zone must
   match its real anatomical footprint.
3. **No polygon topology lines.** The mesh's own construction grid must never be visible.
4. **Front and back both required.** The two highest-activation muscles in the body (gluteus maximus,
   hamstrings) are posterior and were entirely absent from the first studies.
5. **No decorative additions that carry no information.** Explicitly rejected below.

## Rejected treatments (user, 2026-08-07)

| Study | Treatment | Reason rejected |
|---|---|---|
| 01 | Hairline contour on white | White ground rejected outright |
| 04 | Articulated mannequin ball joints | "random circles that add no value" |
| 05 | Fibre-direction hatching | "random lines" |
| 06 | Skeleton armature | "the skeleton adds no value" |

These are removed from consideration permanently. Do not re-propose them.

## Surviving treatments, still open

- Dark field with luminous activation
- Depth-faded lines for far-side zones
- Soft fill with a bright zone edge
- **Opacity-only** — the user's own proposal: the less a muscle is used, the more transparent it becomes.
  Under evidence review (T-058), with particular attention to whether transparency compositing across many
  overlapping zones defeats opacity as a quantitative channel
- Warm luminance ramp versus flat red (F-005)

## Settled encoding (D-020, from `activation-encoding.md`)

- **Brightness carries effort.** Monotonic-luminance warm ramp, dark through amber to bright.
- **Transparency is a supporting channel only**, bounded and always agreeing with brightness, so unused
  muscles still fade toward invisible — preserving the user's original intent.
- **Opacity alone is rejected** as the primary channel: stacked transparent layers are mathematically
  ambiguous (two zones at 50% composite to exactly one zone at 75%), and overlap is the normal condition
  on a see-through body.
- **Depth-based fading as a style is rejected** (D-020) — the user can orbit and zoom in 3D, so a baked
  distance fade is meaningless. Any camera-relative legibility aid is an implementation detail (T-060).
- **Four render states:** active, inactive, uncertain (dashed outline, compressed brightness ceiling so it
  can never look as confident as solid data), never-measured (dotted outline, zero fill, deliberately not
  the ramp's zero-colour).

## Quality bar for the 3D build (D-021 — binding)

The vector studies are retired. They settled the colour system and nothing else. The 3D model must:

1. **Fill each muscle across its full anatomical extent.** Not a strip, not a suggestion — the complete
   footprint of the muscle as it exists on the body.
2. **Outline every zone properly** — clean, continuous, single-weight boundaries in the manner of
   `target-zone-linework.png`.
3. Cover the whole body, front and back, with no bare regions.
4. Show no polygon topology.

## Honest constraint on the interim studies

Hand-authored 2D vector studies cannot reach the quality of the reference images — those are sculpted 3D
meshes. The 2D studies exist **only to decide the treatment**: which colour system, which states, how the
far side reads. They are not a preview of final model quality, and should not be judged as one.

Final quality comes from T-014, which builds actual 3D geometry. The references above are its acceptance
criteria.
