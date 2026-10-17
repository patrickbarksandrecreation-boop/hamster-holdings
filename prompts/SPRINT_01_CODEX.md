# Codex Task — Sprint 01: Hamster Test Chamber

You are the implementation engineer for a new Godot mobile game, **Hamster Holdings**. Read the supplied `docs/ART_BIBLE.md`, `docs/HAMSTER_SPRITE_TEMPLATE.md`, `docs/SPRINT_01.md` and `spec/hamster_animation_manifest_v1.json` before making changes. These are the contracts.

## Objective
Build a **standalone, runnable Godot 4.7.2 / GDScript Android-first portrait prototype** with one hamster, one wheel, one fictional mining computer, deterministic simulation, basic interactions, saved appearance/genome and resumable offline production.

## Scope and guardrails
1. Inspect the working repository. If it is empty, scaffold a new Godot project. If it is a different existing product, **stop and report** rather than modifying it.
2. Create code, scenes, assets and tests that satisfy Sprint 01 acceptance criteria. Keep simulation models pure and separate from scenes/animation.
3. Draw or construct original placeholder pixel assets if approved sprites do not exist. Clearly label placeholders, their owner and exact replacement criteria. Do not copy third-party sprites or use AI-resized illustrations as final pixels.
4. Use `HH-HAM-SYRIAN-01` frame/anchor/animation and phenotype manifest. The code should read manifest data or an equivalent validated source of truth, not duplicate unexplained hard-coded numbers.
5. Seed fixture hamsters Biscuit, Mochi and Pip for phenotype test cases; only Biscuit needs to run in the prototype room.
6. Provide frame-rate-independent fixed-step simulation; a visual state change must reflect actual simulated hamster state. Ensure save data is versioned and local offline catch-up cannot be claimed twice.
7. Follow Android portrait design; retain crisp nearest-neighbour pixel art and test at multiple handset aspect ratios.
8. No pet-store floor, breeding, cloud backend, advertisements, payments, real BTC, or research systems in this sprint. Do not confuse fictional production with financial rewards.
9. Use small, reviewable commits; add automated tests and a short build/readme. Include screenshot proofs and an Android APK smoke test if build/device prerequisites exist. Never claim a test or build that was not performed.

## Required final report
- What changed (files/modules), with concise architecture note.
- Exact test commands run and results.
- APK path or explicit Android-export blocker.
- Screenshot paths, demo walkthrough and known issues.
- Acceptance criteria passed/failed from `docs/SPRINT_01.md`.
- Next two highest-value issues, without beginning Sprint 02.

Before coding, write a brief implementation plan and risks, then proceed unless a missing permission or repository ambiguity would cause changes to a different project.
