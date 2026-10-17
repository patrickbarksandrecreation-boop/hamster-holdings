# Hamster Holdings — Art Bible v1.2
**Status:** Approved direction; implementation specifications are proposed initial standards subject to phone-scale validation.  
**Date:** 2026-10-17  
**Supersedes:** Visual decisions in planning v1.1 where more specific here.

## 1. Locked visual identity
- **Format:** Detailed pixel art in a 2.5D side-on cutaway building, with zoomable rooms.
- **Cast:** Recognisably **natural hamsters**, with anatomically plausible proportions and natural idle/run/rest movement. At specialised stations they demonstrate **exaggerated but charming occupational behaviour**: front paws on controls, sniffing dials, investigating blueprints and celebrating discoveries. They **do not** routinely walk upright, wear full human clothes or become human-shaped characters.
- **World contrast:** Warm, busy, respectable pet store upstairs; cooler, copper-and-teal, disproportionately sophisticated secret hamster-powered fictional Bitcoin mining operation downstairs.
- **Brand anchor:** The hamster wheel and the underground lab should feature in the opening minutes, core camera composition, upgrade silhouettes, iconography and promotional materials.
- **Humour:** Deadpan industrial seriousness about tiny animals and improbable machinery. Expression and scene composition carry most jokes.
- **Care:** Hamsters voluntarily run, take breaks, use enrichment and comfortable habitats. Mechanisms never portray animal mistreatment as efficient play.

## 2. Palette foundations
These are **reference anchors**, not a rigid global palette or final production sprites:

| Usage | Hex |
|---|---|
| Dark outline | `#302C34` |
| Hamster fur shadow | `#765347` |
| Golden coat midtone | `#C18A5B` |
| Golden coat highlight | `#E8C08C` |
| Cream coat | `#F0E2C9` |
| Ear / nose rose | `#D18D8B` |
| Pet-shop warm cream | `#F5E7D1` |
| Pet-shop wood | `#93654C` |
| Pet-shop sage | `#93B79A` |
| Laboratory deep petrol | `#1C4650` |
| Laboratory monitor mint | `#82CFBA` |
| Machinery copper | `#C88354` |
| Alert amber | `#F1BC59` |

Rules: local sprite palettes are intentionally limited; preserve one-pixel intentional clusters, crisp nearest-neighbour textures and readable silhouettes. No auto-antialiased sprite edges, inconsistent outline widths or AI raster paintings downscaled and relabelled as pixel art.

## 3. Core drawing and camera conventions
- Construction reference grid: **16 × 16 artwork pixels** per structural unit. This is not a mandate that every building room be 16 pixels wide.
- Hamster animation canvas: **64 × 48 transparent pixels per frame**. Body occupies approximately **44 × 29 pixels** at rest; extra canvas allows paws, ears and accessories to move without clipping. The 64×48 is a cell, not the size of the animal.
- Canonical local feet / floor anchor: **(32, 42)** in the 64×48 frame. Keep the anchor constant across frames, layers, appearances and actions.
- Draw **right-facing side profile** first. A simple left-facing flip is allowed only for symmetric markings; later asymmetric markings require direction-aware layers.
- All frame data and overlays share the identical 64×48 canvas and foot anchor. Room prop anchors are aligned to the world grid.
- Orthogonal 2D rooms with manually painted depth cues: background wall, rear props, hamster/objects, front props, foreground VFX. Avoid rotating pixel characters in arbitrary 3D perspective.
- Provisional portrait design area: **360 × 640 logical pixels**. Verify Godot viewport rendering/integer scaling, safe areas and different phone ratios; keep readable UI controls independently scalable if needed.
- Nearest-neighbour filtering for sprites; pixel snapping on the world camera; only integer pixel offsets for world sprites. Gameplay camera and UI can have separate render policies where readability requires it.
- Prefer a coarse, consistent pixel outline (usually one artwork pixel) with palette-aware colours rather than pure black everywhere.

## 4. Animal and character design principles
- Primary template: **Syrian hamster**, golden coat, dark eyes, compact rounded body, short legs, recognisable cheek pouches and rounded ears.
- A hamster's **genetic identity is stable**. Coat colour/markings are expressed from saved genotype with deterministic phenotype mapping.
- Job equipment is removable cosmetics or kit: tiny goggles, headsets, control harnesses, identification badges. An accessory is not evidence of intrinsic intelligence.
- Occupational animation uses realistic contact points (front paws, nose), not human arms or fingers.
- Mood is conveyed by pose, ear/eye shapes, pace and pauses, with readable but restrained exaggeration.
- Species variants **must have their own body templates** where anatomical differences matter; never treat every species as a resized Syrian hamster.
- Portraits (planned 96×96) and gameplay sprites must preserve the same defining fur, markings and accessories.

## 5. Layered hamster visual compositor
Bottom-to-top rendering order:
1. Ground shadow (generated by scene, not genetic)
2. Rear legs/ears where occluded
3. Body silhouette + flat fur value masks
4. Genetic coat marking masks (pose-matched)
5. Face, ears, eyes and cheek details
6. Forepaws, including occupational contact poses
7. Gear/accessory overlays (pose-anchored)
8. Optional activity/interaction effects (outside canonical sprite atlas)

**Frame-to-frame alignment rule:** Each layer is authored for each supported pose; do not simply glue a rigid accessory onto arbitrary body frames. Reserve named attachment points such as `head_top`, `neck`, `front_paws`, which are stored per frame.

**Rendering pipeline:** `genotype → deterministic expressed phenotype → pose-specific palette/mask selection → accessories → composited frame`. Never generate a permanent hamster image from a prompt at runtime. Do not save baked sprite image data to a game save; store stable genome, cosmetic state, identifiers and appearance schema version.

## 6. Animation standards
The approved initial animation library and exact production counts are in `docs/HAMSTER_SPRITE_TEMPLATE.md` and machine-readable `spec/hamster_animation_manifest_v1.json`.

- Animation state is driven by the simulation (`resting`, `running`, `operating`, etc.), not by arbitrary visual timers.
- The running wheel is a **separate machine sprite**; its rotation depends on the same simulated wheel activity as the hamster's running animation. In the MVP, a clean loop of pre-drawn indexed wheel frames is preferable to arbitrary texture rotation.
- Occupational animations are composed of tiny natural actions: approach/inspect/paw-touch/pause; do not create a hamster that types like a human.
- For long-distance zoom show simplified animation; at room zoom reveal detailed expressions and paw actions.

## 7. Source-of-truth art pipeline
- Editable pixel-art sources in `art/source/` (`.aseprite` or compatible native source).
- Exported, machine-consumable transparent PNG atlases and JSON metadata in `game/assets/hamsters/`.
- Store palettes, action lists, frame counts, frame anchors and attach points in versioned JSON.
- Use scripted export, atlas validation and contact-sheet regression checks. Generated files should be reproducible from committed source art.
- Original assets only. External reference sprite sheets must **never** be copied into the shipping game unless licensing and provenance have explicitly been reviewed.
- Asset acceptance: expected dimensions/frame counts; transparent pixels around all edges where intended; constant anchors; no clipping on pose/gear variants; consistent palette; no unexpected alpha fringes; readable at normal handset zoom.

## 8. Explicit deferrals
No complete 30+ locus phenotype artwork, no other hamster species, no cybernetic sprite suite, no elaborate shop characters and no dozens of props in Sprint 01. The *schema and compositor* must accommodate future extensions; the *art content* need not exist yet.
