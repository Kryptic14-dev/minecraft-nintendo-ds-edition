# Texture audit and remaining art gaps

Branch: `new-world-system`

## What the source already has

The repository already includes a substantial legacy JoliCraft pack under `dscraft/packs/jolicraft/`. Reuse those assets where their format and renderer support match instead of redrawing duplicates.

- **Environment:** `environment/clouds.png`, `environment/rain.png`, `environment/snow.png`; `misc/water.png`, `misc/watercolor.png`, `custom_water_still.png`; sun/moon are loaded by `source/game/environment.c` from the runtime `misc/` and `textures/` paths.
- **GUI:** existing `gui/background.png`, `gui/container.png`, `gui/crafting.png`, `gui/furnace.png`, `gui/inventory.png`, `gui/icons.png`, `gui/items.png`, `gui/slot.png`, `gui/gui.png`.
- **Mobs:** existing texture candidates for chicken, cow, creeper, pig, sheep, skeleton, spider, and other legacy mobs under `mob/`.
- **Armor:** existing `armor/cloth_1.png` and `armor/cloth_2.png` are the legacy cloth/leather armor sheets; chain, iron, gold and diamond armor sheets are also present. Preserve the old filenames where the current loader expects them. Do not assume the model UVs match a newly named file without checking the armor renderer.
- **Existing terrain/block texture mapping:** `source/game/blocks.c` maps block IDs to coordinates in the current atlas. Most entries after the original block set are placeholders or repeated coordinates; new assets must be packed into the atlas and mapped to IDs, not merely copied into the pack folder.

## Leather armor requirement

Treat the legacy cloth armor set as **leather armor** in the survival item system. Add four wearable equipment slots/items—leather helmet, chestplate, leggings, and boots—with the correct armor points and durability for the Java 1.1-era rules. Reuse `armor/cloth_1.png` and `armor/cloth_2.png` only if the current armor UV mapping confirms those are the intended two-layer sheets. Leather item/inventory icons are a separate requirement if the current GUI cannot crop suitable icons from an existing item atlas.

The current code audit did not find a standalone `source/game/armor.c`; armor behavior must be added to the existing player/inventory/equipment code after locating those definitions. This report does not claim leather armor gameplay is implemented yet.

## Still needed or needs verification

### High priority for the requested world/survival milestone
- **New block atlas tiles, all 8×8 PNGs:** clear glass + 16 stained-glass colours; oak/spruce/birch/jungle/acacia log side, log end and planks (15 tiles); bedrock, coal/iron/gold/redstone/diamond/lapis ores, gravel, sand, sandstone, cobblestone, mossy cobblestone, dirt, grass top/side, stone.
- **Food and drop icons:** apple, bread, raw/cooked pork, raw/cooked beef/steak, raw/cooked chicken, raw/cooked fish, mushroom stew, seeds, wheat, egg, leather drop, feather, wool, bone, string and rotten flesh. Check the existing `gui/items.png` atlas before drawing replacements.
- **Survival HUD:** hearts, hunger icons, hotbar/selection and optional armor icons, unless the existing `gui/` atlas already contains usable equivalents.
- **Crafting/containers:** crafting table, furnace and chest block faces if the new block atlas doesn't already provide them; existing GUI panels can likely be reused.
- **Farming world sprites:** wheat crop growth stages only if the renderer draws crops as sprites rather than block cubes.
- **Mob texture compatibility:** the pack has candidate mob textures, so don't draw replacements yet. Confirm each mesh's UV layout and the expected dimensions first.

### Optional / only if the renderer actually needs them
- Separate glass-pane texture: likely unnecessary if thin panes use the glass tile.
- New sky/cloud/rain/snow art: existing assets are present; verify runtime paths and formats first.
- Extra menu button/world icons: reuse the existing GUI assets where possible.

## Important format and integration notes

- Block/item artwork requested for the new system should be **8×8 pixels** per tile. Existing legacy pack files are various sizes and are not automatically compatible with the 8×8 block atlas.
- The runtime loads PCX files in several places while the pack contains PNGs. Confirm conversion/loading paths before assuming a PNG will be read directly.
- Do not replace the existing atlas wholesale or assign arbitrary UV coordinates. Update the atlas-generation/load pipeline and `source/game/blocks.c` together, then verify on a DS emulator.
- The user's separate texture ZIP was not available as an accessible attachment during this inspection. This audit covers files visible in the GitHub repository; once the ZIP is accessible, compare its filenames and dimensions against this report before declaring any texture missing.
