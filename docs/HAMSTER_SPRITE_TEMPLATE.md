# Hamster Sprite Template — HH-HAM-SYRIAN-01
**Status:** Approved character treatment, proposed exact asset spec for first template.

## Identity and anatomy
- Base character: Syrian hamster (`species_id: syrian`), natural side-profile body, rounded cheeks, short forelimbs and hindlimbs, no long tail, natural quadrupedal walk.
- Canvas per frame: **64×48 RGBA PNG** (transparent). Canonical foot anchor (32,42). Facing right; mirror only symmetric v1 patterns.
- Primary silhouette at relaxed pose: x=10..54, y=12..42, approximate. This is a bounding-box guide and may be adjusted in art approval but cannot change unpredictably by frame.
- Source files: one editable base-poses source and pose-aligned marking/accessory layers; PNG sheets exported by action (64×48 cells) or metadata-described atlas.
- Target in-world display: 1× artwork resolution in viewport, visually about 2× on a typical Android display if viewport scaling allows. Verify readability before committing to a 64×48 budget.

## Approved v1 action library
| Action ID | Frames | Frame rate | Loop? | Content | Delivery |
|---|---:|---:|---|---|---|
| `idle` | 4 | 4 fps | Yes | breathing, ear twitch, occasional blink | Sprint 01 |
| `walk` | 6 | 10 fps | Yes | grounded quadrupedal gait | Sprint 02 |
| `wheel_run` | 8 | 12 fps nominal | Yes | short stride cycle matched to wheel turn; actual playback can vary 8–16 fps | Sprint 01 |
| `rest` | 4 | 3 fps | Yes | curl, subtle breathing | Sprint 01 |
| `groom` | 6 | 8 fps | No | forepaw face-wash animation | Sprint 02 |
| `operate` | 6 | 8 fps | Yes | tiny paws and nose inspect/touch console, never bipedal typing | Sprint 02 |
| `inspect` | 4 | 5 fps | No | curious pause, sniff, lean toward equipment | Later |
| `celebrate` | 6 | 10 fps | No | proud sniff / small happy bob after discovery | Later |

**Wheel machine sprites:** One dedicated **96×96 RGBA** wheel canvas, **8 pre-drawn rotation frames** at **12 fps nominal**, looping only while the simulation says the wheel is being used. Frame selection should derive from a shared simulation wheel-phase value so runner and wheel cannot visibly disagree. Wheel support and connected miner computer are separate static prop layers. One wheel atlas is **768×96 px** when exported as a single horizontal row.

**Atlas convention:** A per-action sprite strip is one row high with width = `64 × action_frame_count` and height = `48` pixels. Examples: `syrian_idle.png` = **256×48**, `syrian_wheel_run.png` = **512×48**, `syrian_rest.png` = **256×48**. Each variant mask uses the exact same dimensions and frame order. A JSON atlas map with individual frames is also allowed if equivalent.

**Delivery contract:** 16 unique base frames in Sprint 01 (`idle` 4 + `wheel_run` 8 + `rest` 4). Full baseline library totals 34 frames (`idle` through `operate`); `inspect` and `celebrate` add 10 later. Accessory and marking layers need only the poses in their current delivery milestone, but must have the same per-frame dimensions and pivots.

**Transitions:** `idle ↔ wheel_run`, `idle ↔ rest` available Sprint 01. Later `idle ↔ walk ↔ operate`, plus one-shot `groom`, `inspect`, `celebrate` returning to idle. No running while the simulated hamster is resting. Render state follows sim state; transitions can wait for the next valid frame but cannot change the simulation.

## Genetically driven appearance slots
1. `species_body_template`: determines torso proportions and allowed poses (Syrian only in Sprint 01).
2. `pigment_locus` → `coat_palette_id`: Sprint 01 golden or cream.
3. `marking_locus` → `marking_mask_id`: Sprint 01 solid or symmetric white band.
4. `eye_appearance`: fixed dark eyes Sprint 01; schema extensible to supported coat/eye interaction genetics.
5. `ear_appearance`: fixed for Sprint 01; species/genetics extensible later.
6. `coat_length`: fixed short fur Sprint 01; long-coat mask/silhouette variants later.
7. `size_class`: visual variance later, without fluid scaling of pixel art; use discrete templates.
8. `accessory_id`: cosmetic equipment layer independent of genetics (no accessory required in Sprint 01).
9. `appearance_seed`: stable cosmetic microvariation only where explicitly allowed, not a substitute for DNA.

**Synthetic test genetics only (do not imply actual Syrian hamster coat genetics):**
- `pigment` alleles `G` and `g`: `G_` → golden, `gg` → cream.
- `marking` alleles `M` and `m`: `M_` → solid, `mm` → symmetric banded mask.
- These stand-ins validate the render pipeline; a biologically researched species model will later supersede them behind a **versioned expression mapping** without erasing existing hamster identities.

Provisional fixture hamsters:
- `biscuit`: `Gg`, `Mm` → golden, solid.
- `mochi`: `gg`, `Mm` → cream, solid.
- `pip`: `Gg`, `mm` → golden, symmetric band.

**No breeding system in Sprint 01.** Fixture genotypes are authored to exercise phenotype derivation and save/load consistency.

## Compositor and alignment validation
- Never stretch or rotate layers to fit a different pose; use pose-aligned layers.
- Keep all animation frame foot anchors exactly (32,42), even if the hamster's nose or ears shift.
- Palette swaps apply to designated mask pixels, not every pixel of a source image.
- Animated overlays track their relevant attachment points per frame; no goggles floating above the face.
- Verify all three fixtures at resting and running poses at normal phone zoom.
- Any asymmetric marking variant must supply true left/right pose masks; do not rely on flipping a lopsided marking.
