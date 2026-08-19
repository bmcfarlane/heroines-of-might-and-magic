# Heroines of Might and Magic — Project Plan

## Design pillars (all decisions trace back to these)

1. **Mechanics untouched.** A HoMM3 veteran plays with full muscle memory. We change meaning, never math (in Phase 1–4).
2. **Nothing scary, nothing gross.** Worst antagonist: a goose with opinions. No death — friends "get tired and go home."
3. **Playable at every commit.** We convert in layers. The game must launch clean (zero VCMI validation errors) on `develop` at all times.
4. **Legally clean.** Zero Ubisoft/NWC assets in the repo. Original art, sounds, and text only. Players supply their own H3 data files.

## Phases

### Phase 1 — The Great Renaming ✅ (v0.1.0, shipped)
Creature/spell/faction name overrides via `core:` specifiers. Meadowbrook (Castle) fully renamed.

### Phase 2 — Full Text Pass (v0.2.x, in progress)
- [x] All nine factions' creature lineups renamed (~139 creatures incl. neutrals) — pending console ID verification
- [ ] Console verification pass: least-confident creature IDs are `zombie`, `faerieDragon`, `efreet`; any load error → GitHub issue
- [ ] All spells + spell descriptions at all skill levels
- [ ] Building names + town name pools per neighborhood ("Griffin Tower" under Fluffy Kittens is the flagship dissonance)
- [x] Meadowbrook Neighborhood Guides (Knights): 8 Heroines named + biographies (P01–P08)
- [ ] Meadowbrook Storykeepers (Clerics): 8 more Heroines (P09–P16) — NOTE: factions have SIXTEEN heroes each, not eight (second counting correction)
- [ ] Hero classes flavor for remaining neighborhoods; primary stats flavor (Kindness/Cheer/Imagination/Curiosity) pending translation-override research
- [ ] Artifacts → Treasures (the Ribbon of Legion, the Cocoa Grail...)
- [ ] Secondary skills flavor (Necromancy → Gardening description text)
- [ ] Map object / bank / event strings
- [ ] Combat log verbs via translation-file override ("attacks" → "cheers at"; "perishes" → "heads home for a nap") — research ticket: which strings live in engine translation JSON vs. hardcoded
- **Exit criteria:** a full playthrough of a random map encounters zero war-flavored English.

### Phase 3 — Art (v0.3.x) ← THE BIG ONE, see ART_SPEC.md
- **3a. Portraits & icons (highest value, lowest risk):** hero portraits, creature icon sets, resource icons. Static single PNGs. AI generation works great here.
- **3b. Adventure map objects:** mines → honey farm / ribbon loom / beachcombing spot / night-meadow; dwellings; decorative objects. Static or 2–3 frame idle loops.
- **3c. Battle sprites:** creature animation frame sets via VCMI's JSON Animation Format (PNG frames, no legacy .def tooling). Meadowbrook's 14 units first.
- **3d. Town screen:** Meadowbrook full town screen with building states.
- **3e. Terrain/UI pastel pass:** recolors, main menu, cursor.
- **Exit criteria per sub-phase:** assets load with zero console errors and read clearly at actual in-game size (test at 100% zoom, not in an image viewer).

### Phase 4 — Sound & Music (v0.4.x)
Encounter jingles, town themes per neighborhood, UI sounds. Ogg/Vorbis only (repo requirement). AI music tools acceptable if license permits redistribution under CC BY-SA.

### Phase 5 — Custom Content (v0.5.x → 1.0)
- Grand Festival Grounds (grail building override) with festival victory text
- Week of the Ladybugs / Week of First Snow / Market Week event flavor
- Cocoa House rumor string pool
- Tutorial map: "The Goose on the Bridge" (map editor deliverable)
- Stretch: true custom factions replacing renames; Encounter verb overhaul if engine/Lua allows

## Design decisions log (binding; future sessions read this first)

1. **2026-08-18 — Nine factions, not seven.** Early docs said seven; H3 Complete has nine. Inferno → Campfire Hollow, Necropolis → Dreamberry Hill.
2. **2026-08-18 — Tone calibration ruling (Emily, design authority).** When a name choice trades between clever/atmospheric and cute/friendly, **cute wins**. Concretely: no moths, no Halloween-adjacent imagery (scarecrows/pumpkins/dusk-spooky), even when "technically gentle." Fluttergrove is butterflies and rainbows; Necropolis is a sleepover (Dreamberry Hill: pillow forts, teddies, Tooth Fairies, Snoring Cloud Dragons). This ruling governs all future text AND all Phase 3 art prompts.
3. **2026-08-18 — Claude ships the complete mod folder every time, never partial/delta zips.** A delta zip caused accidental deletion of Phase 1 files during extraction. Full folder or nothing.
4. **2026-08-18 — Tone is decided empirically by human playtesters** (Emily, Bryan, eventually actual children), not by Claude's aesthetic judgment. Claude proposes; playtest disposes.

## Working agreement (human + Claude)

- **Human owns:** GitHub (repo, issues, merges), playtesting, running image generation, screenshots back to Claude, legal/licensing checks on generated assets.
- **Claude owns:** all JSON/config authoring, specs, prompt engineering, text content, debugging from console output, keeping this plan current.
- **Loop:** one sub-phase per session → Claude produces files → human commits to a feature branch → playtest → console/screenshot feedback → fix → merge to `develop`.
- **Issue discipline:** every console validation error becomes a GitHub issue before it gets fixed. Yes, even the one-line ones. Especially the one-line ones.

## Risks

| Risk | Mitigation |
|---|---|
| AI image inconsistency across a unit's animation frames | Character-sheet strategy + heavy downscale (see ART_SPEC.md §3) |
| Combat verbs hardcoded in engine | Fallback: accept them in v1; upstream a translation-key PR to VCMI later |
| Scope explosion (7 towns × 14 units × ~15 anim groups) | Meadowbrook-first; other factions stay renamed-with-original-art until 3c proves the pipeline |
| Trademark | Repo contains only original assets; name is parody/fan-work but keep "unaffiliated" disclaimers everywhere; rename if ever asked |
