# Texture audit and remaining implementation gaps

Branch: `new-world-system`

## User-provided texture ZIP checked

Inspected `MCDS Textures(1).zip`: it contains 177 PNG files. The ZIP includes glass, leather armor, colored wool, many 8×8 block tiles, food/drop icons, tool icons, and crafting-table/furnace face textures. **Do not ask for or list glass or leather armor textures as missing.** The remaining work is to integrate these assets into the game and confirm each is compatible with its renderer.

### Confirmed useful files in the ZIP

- **Glass:** `glass.png` (8×8).
- **Leather armor:** `leather_helmet.png`, `leather_helmet_overlay.png`, `leather_chestplate.png`, `leather_leggings.png`, `leather_leggings_overlay.png`, `leather_boots.png`, `leather_boots_overlay.png`; `leather.png` item/drop icon. These are 8×8 files in the ZIP. Verify whether these are intended as item icons or model skin/UV textures before connecting them to worn armor rendering.
- **Wool:** white, orange, magenta, light blue, yellow, lime, pink, gray, light gray, cyan, purple, blue, brown, green, red and black wool tiles (8×8).
- **Blocks/ores:** bedrock, coal ore, iron ore, gold ore, redstone ore, diamond ore, lapis ore, gravel, sand, sandstone and its top/bottom, cobblestone, mossy cobblestone, dirt, grass, grass-block side/overlay, stone, plus several utility blocks.
- **Food/drops:** apple, beef, porkchop, chicken, cooked chicken, cooked porkchop, cod/cooked cod, bread, golden apple, mushroom stew, wheat, wheat seeds, egg, feather, bone, string, rotten flesh and leather.
- **Tools/armor items:** wooden, stone, iron, gold and diamond tool icons, plus leather/iron/gold/diamond armor item icons.
- **Block faces:** crafting table front/side/top and furnace front/front-on/side/top.
- **Larger interface or block sheets:** e.g. `icons.png`, `widgets.png`, `tabs.png`, `tab_inventory.png`, `tab_items.png`, `tab_item_search.png`, `stats_icons.png`, and 256×256 crafting/furnace/anvil/enchanting-table images. These are not individual 8×8 tiles and should be used only where the corresponding UI/rendering code expects a full sheet.

## What may still be missing

### Block tiles / environment
- The ZIP's glass and wool tiles are present, but **16 separate stained-glass block textures are not evident** from the filenames; only `glass.png` is present. If stained glass is required as separate colors, add those tiles or implement tinting if the renderer supports it.
- The requested five wood families still need checking: oak/spruce/birch/jungle/acacia log sides, log ends and planks. Those filenames were not evident in the ZIP listing.
- Confirm all needed terrain tiles and map them to block IDs: some useful tiles are present, but do not assume every requested block face has a matching texture.
- Leaves for each wood type, cactus/reeds/tall grass/flowers/mushrooms/torch/ladder/rails/doors/trapdoors/fences may still be needed depending on which blocks are implemented.
- Water/lava/fire textures should be checked against the existing runtime assets before drawing replacements.

### Food, farming, and mob art
- Many food and drop icons are present. Check whether raw fish variants, cooked beef/steak naming, and every item required by the chosen Java 1.1-era feature set have matching assets.
- The ZIP has sweet berry bush stages, which are modern art and not a Java 1.1 feature; don't implement berries just because the files exist unless requested.
- Wheat crop growth stages 0–7 were not evident by filename. Add them only if the crop renderer requires separate stage textures.
- The repository's legacy pack already has mob texture candidates for pig, cow, chicken, sheep, zombie, skeleton, spider and creeper. Inspect model UV dimensions before requesting or integrating replacement mob sheets.

### HUD and menus
- The ZIP includes several larger GUI sheets, but dedicated heart/hunger/hotbar/armor sprites were not obvious as standalone filenames. Inspect the existing interface atlas and current sprite mapping first; only draw missing sprites after confirming the atlas does not already provide them.
- World creation/list/delete UI icons are optional until the world menu code is in place.

## Leather armor implementation requirement

Use the provided leather armor assets; do not request new leather armor art. Implement four wearable items (helmet, chestplate, leggings, boots), armor slots, protection, durability, equip/unequip behavior, and saving/loading. Check the current player/inventory structures and existing renderer UV mapping before choosing whether the ZIP's 8×8 armor images are item icons only or can be used as worn armor textures. The presence of art does **not** mean the gameplay code is already implemented.

## Integration notes

- The intended block/item tile size is **8×8 pixels**. The ZIP contains 177 PNGs of mixed sizes: most named block/item tiles are 8×8, while some GUI sheets and armor color/skin files are larger. Keep these formats distinct.
- The source's block renderer maps block IDs to coordinates in an atlas (see `source/game/blocks.c`). Copying PNGs into the repository alone will not make them appear in game; atlas loading/packing and block ID/UV mapping must be updated together.
- Some runtime paths use PCX textures and custom texture loading. Verify the asset conversion and runtime path requirements rather than assuming every PNG can be opened directly.
- This audit covers the provided ZIP plus files visible in the repository. It does not claim that these assets have already been integrated or that leather armor gameplay is complete.
