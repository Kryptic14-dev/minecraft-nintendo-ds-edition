# Texture Asset Plan

This is the art handoff for the new-world-system branch. The game currently samples a 8-by-8 tile atlas: each tile is 8x8 pixels (the atlas dimensions must be confirmed from the source assets). Before drawing the final atlas, keep each requested tile as an individual 8x8 PNG so it can be packed into the project's actual atlas without overwriting existing tiles. The existing atlas layout must be checked before assigning final coordinates.

## Art rules

- Base tile: **8x8 pixels**, pixel art, crisp edges, no smoothing.
- Make each texture tileable on all edges unless the entry says otherwise.
- Keep transparent pixels genuinely transparent for glass; don't paint a checkerboard background.
- For glass, use a subtle tint, thin bright edge highlights, and very little opaque fill. Avoid relying on alpha alone: the DS renderer may need an opaque/tinted fallback.
- For logs, draw the end-grain ring texture separately from the bark texture.
- Save working files as PNG. Do not scale them up with smoothing.
- Names below are source filenames for the art handoff, not guaranteed final in-game filenames or atlas coordinates.

## Priority 1 — glass

Make these 17 individual 8x8 tiles:

- [ ] `glass_clear.png` — clear glass face, faint cool tint and edge highlight.
- [ ] `glass_white.png`
- [ ] `glass_orange.png`
- [ ] `glass_magenta.png`
- [ ] `glass_light_blue.png`
- [ ] `glass_yellow.png`
- [ ] `glass_lime.png`
- [ ] `glass_pink.png`
- [ ] `glass_gray.png`
- [ ] `glass_light_gray.png`
- [ ] `glass_cyan.png`
- [ ] `glass_purple.png`
- [ ] `glass_blue.png`
- [ ] `glass_brown.png`
- [ ] `glass_green.png`
- [ ] `glass_red.png`
- [ ] `glass_black.png`

For all stained glass, preserve a visible transparent centre and tint the borders/edges with the matching colour. Black stained glass should be dark smoky glass, not a fully solid black square.

**Panes:** no separate pane texture is required for the first implementation if panes are rendered using the same glass tile on a thinner shape. If the renderer cannot support thin geometry, we may need dedicated pane sprites later; don't spend time drawing those yet.

## Priority 2 — five wood families

For each wood type, make a bark-side tile and an end-grain tile. Planks are a third tile per type. That's 15 tiles total.

| Wood | Bark tile | Log end tile | Planks tile |
|---|---|---|---|
| Oak | `log_oak_side.png` | `log_oak_end.png` | `planks_oak.png` |
| Spruce | `log_spruce_side.png` | `log_spruce_end.png` | `planks_spruce.png` |
| Birch | `log_birch_side.png` | `log_birch_end.png` | `planks_birch.png` |
| Jungle | `log_jungle_side.png` | `log_jungle_end.png` | `planks_jungle.png` |
| Acacia | `log_acacia_side.png` | `log_acacia_end.png` | `planks_acacia.png` |

- [ ] Oak bark/end/planks
- [ ] Spruce bark/end/planks
- [ ] Birch bark/end/planks
- [ ] Jungle bark/end/planks
- [ ] Acacia bark/end/planks

## Priority 3 — world generation and survival

These are needed for the broader feature plan. Existing atlas entries may already cover some of them; check the current pack before drawing duplicates.

- [ ] `bedrock.png` — dark, irregular stone texture.
- [ ] `coal_ore.png` — stone with black coal flecks.
- [ ] `iron_ore.png` — stone with tan/brown iron flecks.
- [ ] `gold_ore.png` — stone with yellow-gold flecks.
- [ ] `redstone_ore.png` — stone with red flecks.
- [ ] `diamond_ore.png` — stone with cyan flecks.
- [ ] `lapis_ore.png` — stone with deep-blue flecks.
- [ ] `gravel.png` — loose grey/brown pebbles.
- [ ] `sand.png` — pale granular sand.
- [ ] `sandstone.png` — layered sandy stone.
- [ ] `cobblestone.png` — irregular grey stones.
- [ ] `mossy_cobblestone.png` — cobble with green moss.
- [ ] `dirt.png` — brown soil.
- [ ] `grass_top.png` — green grass top.
- [ ] `grass_side.png` — dirt side with a green grass lip.
- [ ] `stone.png` — neutral grey stone.

## Optional later art

Only make these after the first glass/wood integration is underway:

- [ ] 16 wool tiles: `wool_white.png`, `wool_orange.png`, `wool_magenta.png`, `wool_light_blue.png`, `wool_yellow.png`, `wool_lime.png`, `wool_pink.png`, `wool_gray.png`, `wool_light_gray.png`, `wool_cyan.png`, `wool_purple.png`, `wool_blue.png`, `wool_brown.png`, `wool_green.png`, `wool_red.png`, `wool_black.png`.
- [ ] Bed top/side/end textures for the same 16 colours. Beds are two-block objects, so their art may need multiple faces rather than one cube tile.
- [ ] Crafting table side/top, furnace side/front/top, chest side/front/top.
- [ ] Tool icons for wooden, stone, iron, gold and diamond pickaxes, axes, shovels and swords.
- [ ] Simple low-resolution icons for inventory slots and the hotbar, if the existing UI doesn't already have suitable art.

## Important integration note

Please don't pack tiles into arbitrary atlas positions yet. The game maps block IDs to atlas coordinates in `source/game/blocks.c`, and texture UVs are generated from that atlas. We need to reserve free coordinates and map each new block to the correct tile before the art can appear in-game. The first implementation should prioritize clear glass plus the 16 stained-glass tiles and the five wood families.


## Priority 4 — food, farming, and item icons

These are **inventory/item icons**, not block-face textures. Draw each as a centered 8x8 pixel-art PNG with transparent background. The names are proposed source filenames; they still need to be connected to the game's item/inventory code.

### Starter food loop

- [ ] `food_apple.png` — apple.
- [ ] `food_bread.png` — loaf of bread.
- [ ] `food_raw_porkchop.png` — raw porkchop.
- [ ] `food_cooked_porkchop.png` — cooked porkchop.
- [ ] `food_raw_beef.png` — raw beef.
- [ ] `food_steak.png` — cooked beef/steak.
- [ ] `food_raw_chicken.png` — raw chicken.
- [ ] `food_cooked_chicken.png` — cooked chicken.
- [ ] `food_raw_fish.png` — raw fish.
- [ ] `food_cooked_fish.png` — cooked fish.
- [ ] `food_mushroom_stew.png` — stew in a bowl.
- [ ] `food_golden_apple.png` — optional rare food.

### Farming and animal drops

- [ ] `item_wheat_seeds.png` — wheat seeds.
- [ ] `item_wheat.png` — harvested wheat.
- [ ] `crop_wheat_stage_0.png` through `crop_wheat_stage_7.png` — 8 tiny crop growth stages, if crops are rendered as world sprites.
- [ ] `item_egg.png` — chicken egg.
- [ ] `item_leather.png` — leather drop.
- [ ] `item_feather.png` — feather drop.
- [ ] `item_wool_white.png` — wool drop/item icon (colored wool variants can reuse the 16 wool color set above).
- [ ] `item_bone.png` — skeleton drop.
- [ ] `item_string.png` — spider drop.
- [ ] `item_rotten_flesh.png` — zombie drop.

For a first playable survival build, prioritize the ten basic foods (apple, bread, raw/cooked pork, raw/cooked beef, raw/cooked chicken, raw/cooked fish) plus wheat/seeds and egg. Other drops can follow.

## Priority 5 — mob art

**Do not draw full mob sheets yet.** Unlike block tiles and item icons, mob textures must match the model UV layout and the animation/mesh code in this project. A nicely drawn texture with the wrong UV layout will appear scrambled in-game. First-pass mob list, ordered for a low-population DS build:

1. Passive animals: `mob_pig`, `mob_cow`, `mob_chicken`, `mob_sheep`.
2. Hostile mobs: `mob_zombie`, `mob_skeleton`, `mob_spider`, `mob_creeper`.

Target mob features: idle/walk animations; animals wander and flee; zombies pursue the player; skeletons use a simple ranged attack only if the existing combat code supports it; spiders pursue and jump only if performance allows; creepers approach and explode only if a safe, low-cost behavior can be implemented. Keep spawn counts low and configurable.

Before making these textures, we'll inspect the existing model dimensions and UVs and give you exact canvas sizes and filename conventions for each mob. For now, you can make concept sprites, but don't commit final-sized mob sheets yet.
