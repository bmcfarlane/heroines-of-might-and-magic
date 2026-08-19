# Heroines of Might and Magic

A cozy total-conversion mod for [VCMI](https://vcmi.eu), the open-source Heroes of Might and Magic III engine. Same beloved mechanics — exploration, weekly rhythms, town building, tactical hex encounters — reimagined as a friendly world of neighborhoods, festivals, shy creatures, and snacks.

**Design pillar:** a HoMM3 veteran can play with total muscle memory; an eight-year-old never encounters anything scarier than a goose with opinions.

## Requirements

1. [VCMI](https://vcmi.eu/download/) installed and working.
2. The original Heroes III data files (VCMI requires them; buy the Complete Edition on GOG).

## Installing the mod (manual, for now)

1. Find your VCMI `Mods/` directory:
   - Windows: `Documents\My Games\vcmi\Mods`
   - Linux: `~/.local/share/vcmi/Mods`
   - macOS: `~/Library/Application Support/vcmi/Mods`
2. Copy this entire folder in, so you have `Mods/heroines-of-might-and-magic/mod.json`.
3. Open the VCMI Launcher, find "Heroines of Might and Magic" in the mod list, and enable it.
4. Start a new game. Welcome to Meadowbrook.

## What works in v0.2 (Phase 2 in progress)

- All **nine** neighborhoods named (Meadowbrook, Fluttergrove, Sweetshop Lane, Campfire Hollow, Dreamberry Hill, Music Quarter, Craft District, Tidewhisper Cove, Starlight Observatory)
- All ~139 creatures renamed — every faction lineup plus neutral map friends
- A starter set of spells converted to Songs & Games
- Original sprites/portraits still show (art is Phase 3); combat verbs like "perishes" still stock (translation override in progress)
- Everything converts in layers and the game stays playable at every commit

## Roadmap

- **Phase 2 — Full text pass (in progress):** creatures ✅. Still to do: hero names/biographies, spell descriptions, artifacts, building names, town name pools, map object strings, and combat verbs ("attacks", "perishes") via engine translation-file overrides — tracked in issues.
- **Phase 3 — Art:** creature sprites (VCMI accepts PNG frame sets via its JSON [Animation Format](https://vcmi.eu/modders/Animation_Format/), no .def tooling needed), town screens, terrain recolors toward a pastel palette.
- **Phase 4 — Sound & music:** encounter jingles instead of battle music (Ogg/Vorbis, per repo rules).
- **Phase 5 — Custom content:** the Grand Festival Grounds grail building, Week of the Ladybugs event pool, Cocoa House rumor strings, and eventually fully custom neighborhood factions rather than renames.

## Contributing

Text contributions are the easiest on-ramp: pick any `core:` object not yet converted, add an override in the matching `Content/config/heroines/*.json` file, keep it kind, keep it funny, open a PR. Check the VCMI console on game load — the mod must produce zero validation errors.

## Legal

This mod contains no Ubisoft/NWC assets and requires a legally owned copy of Heroes III. "Heroes of Might and Magic" is a trademark of Ubisoft Entertainment; this is an unaffiliated fan project. Mod content is licensed CC BY-SA 4.0.
