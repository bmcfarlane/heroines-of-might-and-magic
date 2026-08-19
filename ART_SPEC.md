# Heroines — Art Specification & AI Generation Pipeline

This document is the single source of truth for every PNG in the project. Read §1–3 before generating anything. The inventory (§4) and the prompt template (§5) depend on them.

## 1. Global style bible (paste into EVERY image prompt)

> **STYLE BLOCK (do not vary between images):**
> "Storybook watercolor-and-gouache illustration style, soft pastel palette (mint green, butter yellow, powder blue, blush pink, cream), warm morning light, thin dark-chocolate-brown outlines, rounded friendly shapes, no sharp points anywhere, gentle painterly texture, in the spirit of classic 1990s isometric fantasy game art but cozy instead of grim. Absolutely no text, no watermark, no signature, no border, no drop shadow."

Rules:
- **One style block, forever.** Consistency across 200+ assets comes from never editing this paragraph. If we want a style change, we version it (STYLE v2) and regenerate *everything* affected. No mixing.
- **Palette anchor:** when a specific asset needs extra colors (a red ladybug), they're *added to* the block for that asset, never substituted.
- **Tone ruling (2026-08-18, binding):** cute beats atmospheric, always. No moths, no Halloween-adjacent motifs (scarecrows, pumpkins, spooky dusk). Dreamberry Hill art is sleepover-cozy: pillow forts, teddies, nightlights, warm lamplight. If a prompt could be read as "hauntingly beautiful," rewrite it until it reads "huggable."
- **Outline color** is dark brown (#3D2B1F-ish), never black — black outlines read "harsh" at small sizes against pastel fills.

## 2. Engine constraints (why the specs below look the way they do)

- **Format:** PNG with real alpha transparency. Every asset. Request "isolated on transparent background" and *verify* — some generators fake transparency with white or checkerboard. A checkerboard-patterned duckling in-game is a bug we will only make once.
- **The downscale is the great equalizer.** We generate at 1024×1024 (or the generator's native size) and downscale to target size in the pipeline. This hides AI artifacts and enforces cohesion. Never ask the generator for tiny sizes directly — small-size generation is where AI art falls apart.
- **Canvas discipline:** battle creature frames sit on a fixed-size canvas with the creature occupying a consistent footprint and the "feet" at a consistent anchor point. The character must be **full body, entirely inside frame, nothing cropped** — a cropped ear means the asset is unusable, not fixable.
- **Facing:** battle sprites face RIGHT (the engine mirrors for the other side). All battle-pose prompts must say "facing right in three-quarter view."
- **Adventure map is tile-based (32×32 px tiles).** Map objects are drawn on canvases that are multiples of 32. They're viewed top-down-ish at a slight angle — prompt for "slight bird's-eye three-quarter angle."
- **Readability test:** every asset gets viewed at final in-game size before acceptance. If you can't tell the Duckling from the Fancy Duckling at 100% zoom, the hat isn't big enough. Iterate on silhouette, not detail.
- **Animation reality check:** AI generators cannot produce consistent multi-frame animation of the same character. Our strategy (§3) is built around this limitation, not in denial of it.

## 3. The three-tier animation strategy

**Tier A — Static (Phase 3a/3b):** portraits, icons, map objects. One image each. AI-native territory. We do ALL of Tier A before touching Tier B.

**Tier B — "Puppet-minimal" battle sprites (Phase 3c):** For each creature we generate ONE master pose (standing, facing right) plus TWO variants via the character-sheet trick: prompt the generator for *one image containing a 2×2 character sheet of the same character: standing / eyes closed mid-bounce / leaning forward happily / sitting down pleased* — same sheet, same generation, so the character stays consistent. We then crop the sheet into frames and map them to VCMI animation groups generously (standing group = frames 1+2 alternating; "attack" = lean-forward; "getting hit"... is "pleasantly surprised"; "death" = sitting down pleased, because nobody dies, they sit down and are pleased). It will look like a lively paper-puppet theater. For our aesthetic that is a *feature* — cozy games (Paper Mario, cardboard theater) have proven this style.

**Tier C — Real animation (post-1.0, human artists or future tools):** proper walk cycles. Not planned; noted so nobody thinks we forgot.

## 4. PNG Inventory — Phase 3a + Meadowbrook 3b/3c

### 4.1 Hero portraits (Tier A) — 16 images
Two sizes derive from one master each (generate once, downscale twice: large portrait + small portrait).

| ID | Heroine | Prompt subject core |
|---|---|---|
| P01 | Marigold (was Sir Christian) | girl with marigold-orange braids, straw sun hat, holding a picnic basket, freckles, gap-tooth grin |
| P02 | Sorsha-Jump | athletic girl mid-laugh, jump rope over shoulder, high ponytail, medal pinned crooked |
| P03 | Bea | round girl in beekeeper veil pushed up, honey-dipper wand, three bees as friends |
| P04 | Petal | small girl completely covered in ladybugs, delighted about it |
| P05 | Captain Puddle | girl in yellow raincoat and boots, holding an enormous leaf as umbrella for a duckling |
| P06 | Nan | grandmotherly guide with cocoa mug, cardigan of many pockets, knowing smile |
| P07 | Juniper | tall quiet girl with a pet goose (the goose looks skeptical) |
| P08 | Twyla | girl with star-chart bandana, telescope, stardust freckles that faintly glow |
| P09–P16 | reserved: Fluttergrove lineup | spec'd in Phase 2 when biographies are written |

### 4.2 Creature icons, Meadowbrook (Tier A) — 14 images
Small square icon per unit: bust/face only, centered, big readable silhouette.
Ducklings ×2 (plain / tiny top hat), Bubble Blowers ×2 (one wand / double wand), Fluffy Kitten / Winged Kitten, Picnic Planner / Party Planner (clipboard / clipboard+balloons), Storyteller / Grand Storyteller (book / enormous pop-up book), Pony Rider / Show Pony Rider (pony / pony with ribbons), Unicorn Friend / Rainbow Unicorn.

### 4.3 Resource icons (Tier A) — 7 images
Coin (gold), craft sticks (wood), river stones (ore), honey jar (sulfur), ribbon spool (mercury), seaglass (crystal), stardust vial (gems). Each: single object, centered, slight glow, icon-like clarity.

### 4.4 Adventure map objects (Tier A/B) — first batch, 6 images
Honey farm (mine), ribbon loom cottage (mine), beachcombing spot (mine), night-meadow with fireflies (mine), Meadowbrook duckling pond dwelling, the Bridge Goose (map guardian, one static pose of maximum opinion).

### 4.5 Battle sprites, Meadowbrook (Tier B) — 14 character sheets
One 2×2 character sheet per unit (poses per §3). Full body, facing right, feet on an imaginary common ground line. These 14 sheets are the entire animation budget for the faction — that's the point.

**Phase 3a total: 43 generated images. With rerolls, budget ~120 generations.** Anything beyond a 3:1 reroll ratio means the prompt is wrong — stop and fix the prompt, don't brute-force.

## 5. The prompt template (for ChatGPT image generation, Aug 2026)

```
Generate a PNG image, transparent background, 1024×1024.

[STYLE BLOCK — paste §1 verbatim]

SUBJECT: [subject core from inventory, e.g. P05]

COMPOSITION: [pick one]
- Portrait: "head and shoulders, centered, facing slightly left, warm eye contact, plain transparent background"
- Icon: "bust only, perfectly centered, bold simple silhouette readable at 32 pixels, transparent background"
- Map object: "whole building/scene from slight bird's-eye three-quarter angle, compact footprint, transparent background"
- Battle sheet: "a 2×2 character reference sheet of THE SAME character in 4 poses: standing relaxed / mid-bounce with eyes closed / leaning forward with delight / sitting down looking pleased. Full body in every pose, all facing right in three-quarter view, feet aligned on a common invisible ground line, generous margin around every pose, transparent background"

HARD CONSTRAINTS (repeat even though the style block says so — repetition works):
no text, no watermark, no border, no cropping of the character, entire subject inside frame, true transparent background (not white, not checkerboard).
```

Workflow per asset: generate → check transparency in an actual editor → check silhouette at target size → accept or reroll with ONE changed clause → log the accepted prompt verbatim in `art/prompts.log` (reproducibility is non-negotiable; future-us will thank present-us).

## 6. Repo layout for art

```
art-source/          # accepted 1024px masters + prompts.log (in repo, CC BY-SA)
Content/data/        # downscaled, engine-named bitmaps
Content/sprites/     # battle frames + VCMI animation JSON (Claude authors the JSON)
```

Claude authors all animation-format JSON once frames exist; human never has to touch frame-index mapping. Exact target pixel dimensions for each engine slot get filled into §4 tables during Phase 3a setup, verified against the VCMI Animation Format docs and a live console — dimensions in docs trust-but-verify, dimensions in a running engine are truth.
