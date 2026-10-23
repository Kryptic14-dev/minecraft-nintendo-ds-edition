# Implementation Checklist — Nintendo DS Survival Edition

This checklist tracks the requested scope. A checked item means implemented and verified; planned requirements are deliberately unchecked.

## Milestone 1 — Worlds and renderer stability
- [ ] Fix world-list scanning for both bundled NitroFS worlds and external SD/card worlds; stat full paths and safely handle missing directories.
- [ ] Add a world creation flow with a name and seed.
- [ ] Define a versioned world metadata format without corrupting legacy `.world` saves.
- [ ] Generate a seeded world, load it in the existing renderer, and establish a safe spawn.
- [ ] Save block changes and player state, then reopen the same world.
- [ ] Test world listing, opening, saving, and reopening in DeSmuME and melonDS.

## Milestone 2 — Vertical world and terrain
- [ ] Set Y = 0 as sea level throughout generation and gameplay.
- [ ] Support the target vertical range Y = -60 through Y = 80.
- [ ] Place unbreakable bedrock at Y = -60.
- [ ] Generate terrain above and below sea level, with water at sea level.
- [ ] Generate caves and depth-weighted coal, iron, and other ore deposits.
- [ ] Update storage, collision, culling, and rendering for the expanded height without exceeding DS memory limits.

## Milestone 3 — Building blocks
- [ ] Wool in white, orange, magenta, light blue, yellow, lime, pink, gray, light gray, cyan, purple, blue, brown, green, red, and black.
- [ ] Beds in all 16 colors, with two-block placement and correct breaking behavior.
- [ ] Clear glass and stained glass in all 16 colors.
- [ ] Clear glass panes and stained-glass panes in all 16 colors, with thin collision and connections where practical.
- [ ] Add block IDs, texture mapping, drops, placement rules, and save compatibility together.

## Milestone 4 — Survival loop
- [ ] Mining, placement, block drops, and inventory.
- [ ] Hotbar and item selection.
- [ ] Health, hunger, fall damage, death, and respawn.
- [ ] Tools with durability and mining-speed differences.
- [ ] Basic crafting and progression.
- [ ] Day/night cycle and mob spawn rules.
- [ ] A small, performance-limited hostile mob population.
- [ ] Chests and furnaces if memory, controls, and engine support permit.

## Milestone 5 — Build and verify
- [ ] Automated `.nds` build succeeds from the feature branch.
- [ ] ROM boots to the menu in DeSmuME and melonDS.
- [ ] A newly generated world renders and can be explored without crashing.
- [ ] Save/reload preserves terrain and player changes.
- [ ] Check memory use and frame rate on representative DS/emulator settings.

## Known caution
The current engine has fixed-size cluster-column storage and a legacy world format. The expanded negative-to-positive Y range cannot be safely claimed until storage, world I/O, renderer assumptions, and collision code have been traced and changed together. The list above is the target, not a claim of completion.
