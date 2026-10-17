# Sprint 01 — The Hamster Test Chamber
**Timebox:** 2 weeks (planning target; revisit after initial asset estimates).  
**Goal:** An installable portrait Android proof of the hamster+wheel loop, with deterministic simulation, readable pixel artwork and reliable saved identity.  
**Project:** Separate new `Hamster Holdings` Godot repository, **not** either existing website or daycare repo. No remote repo creation/changes until the developer chooses a destination.

## Scope: committed work
1. **Godot project:** Pin Godot 4.7.2 stable for the first sprint; GDScript; landscape not required. Create clean project structure and reproducible launch instructions.
2. **One prototype room:** A side-on 2.5D-style hamster test chamber with a habitat, a wheel connected by visibly silly power-transmission parts to one fictional crypto-mining computer, readable production counter and minimalist HUD.
3. **One gameplay hamster:** Named `Biscuit`, stable ID, synthetic genotype, expressed phenotype, energy, rest/run state, and speed/endurance values. Fixture hamsters `Mochi` and `Pip` only needed for automated appearance previews/tests, not to populate the room.
4. **Minimal art:** Original Syrian-hamster base and pose-aligned palette/mask variations. Required Sprint 01 animations are `idle` (4), `wheel_run` (8), `rest` (4). Wheel loop comprises 8 frames at 96×96 and is phase-synchronised with the simulated wheel; it animates only when the actual simulation is generating wheel power. Temporary original placeholder art may be used only if clearly marked and included in an asset replacement task before visual approval.
5. **Simulation:** Fixed-step deterministic state model independent of on-screen drawing and frame rate. A hamster alternates wheel running and appropriate rest based on energy thresholds. Fictional power is accumulated from hamster state and wheel efficiency. Seeded RNG if needed; tests cannot rely on unseeded randomness.
6. **Interaction:** Tap hamster to view name, energy, speed, endurance, role and current activity. Provide a clearly labelled prototype control to pause/restart wheel assignment, a simple wheel upgrade and visually responsive virtual production. Controls should be usable on an Android portrait display.
7. **Persistence:** Local save/load of identifiers, genome, schema versions, stats, resources, assignment, simulation timestamp and RNG state (if randomness is used). A short offline catch-up should use the same simulation logic as active progression, not a completely separate economy.
8. **Validation:** Headless Godot startup/import checks, unit tests for pure simulation and phenotype derivation, save-load fixture test, visual screenshot/contact-sheet review and Android debug build if SDK is available.

## Out of scope (do not silently add)
Pet-store floor, adoption, research tree, actual breeding, complex networks, SqueakScripts, multiple facilities, payments, ad SDKs, Bitcoin wallets, analytics SaaS, Supabase, shop staff or paid cosmetics. The project architecture must permit their later addition without implementing them now.

## Suggested work packages
**S1.1: Bootstrap and contracts (2–3 days)**
- Godot project, launch/test commands, folder structure, JSON schema/spec import validation and test harness.
- Suggested folders: `game/scenes/`, `game/scripts/simulation/`, `game/scripts/appearance/`, `game/scripts/persistence/`, `game/assets/hamsters/`, `art/source/`, `tests/`, `docs/`.
- Deliver: blank room with camera and placeholder UI rendered correctly in portrait.

**S1.2: Pure simulation (2–3 days)**
- Hamster model, wheel model, fixed-step updater and rested/running state transitions.
- Unit tests for energy bounds, id stability, reproducibility and output consistency across chunk sizes.

**S1.3: Hamster sprite and scene (3–5 days)**
- Original Syrian hamster animation art, palette swap/mask renderer, wheel animation, state-to-animation binding, normal-size on-phone legibility review.
- Three appearance fixtures must render with consistent anchors and no clipping.

**S1.4: Save, offline and Android QA (2–3 days)**
- Versioned local save, resume simulation, touch inspection panel, debug package and device smoke tests.
- Update known defects and backlog; do not claim a debug APK works until installed and opened on an actual device.

## Objective acceptance criteria
- [ ] Project opens and runs in the pinned Godot version, with no fatal startup errors.
- [ ] At least one hamster visibly alternates `wheel_run` and `rest` from simulation state, and the wheel responds in sync.
- [ ] Production increases **only** when energy/state and machine assignment permit it. A pause prevents new power production.
- [ ] Changing render frame rate or hiding the scene does not change simulation outcome for the same game-time duration.
- [ ] Running a deterministic 300-second test once matches running the same seeded 60-second test five times, within stated numerical tolerance.
- [ ] `biscuit`, `mochi`, `pip` express the expected fixture coat/marking variants, with consistent pose alignment.
- [ ] Saving, closing and reopening preserves Biscuit's name, genome, appearance, resources, assignment and current simulation state.
- [ ] A controlled offline gap (e.g., 5 minutes) resumes with valid resource and energy values; no double-crediting if loaded twice.
- [ ] Buttons have practical mobile touch targets; UI readable on a real midrange Android handset.
- [ ] An Android debug APK is built and smoke-tested on device, or the delivery explicitly identifies missing SDK/hardware prerequisites rather than pretending validation happened.
- [ ] No crypto payout/ad SDK/network permissions included.
- [ ] Agent provides commits/PR, test commands and logs, screenshots and a concise deviations list.

## Required architectural contracts
- Simulation state must remain serialisable independent of Godot Nodes, sprites and camera position.
- Character appearance must be deterministically derived from versioned genotype data.
- Renderer can swap visuals without altering hamster simulation or saved identity.
- Production calculations use fictional game currency, never actual Bitcoin units.
- Later research, genetics and automation must plug into explicit models/events, not gameplay calculations buried in UI scripts.

## Definition of done and next gate
**Done:** User can install a debug APK, watch Biscuit run/rest in sync with production, inspect his attributes, upgrade one piece of equipment and reopen the game with identical identity and consistent progression. 
**Next gate:** Do players enjoy watching and controlling one hamster for a few minutes? If not, refine the wheel feedback, hamster expressiveness and interactions before building shop systems.
