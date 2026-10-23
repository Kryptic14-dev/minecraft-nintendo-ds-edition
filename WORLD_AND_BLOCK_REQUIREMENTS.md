# World and Building-Block Requirements

This document records the gameplay requirements for the new-world implementation. It is a target specification, not a claim that every feature is already implemented.

## World coordinates

- **Y = 0 is sea level.** Terrain generation, water level, cave depth, ore distribution, and spawn placement must all use this shared reference.
- Target buildable range: **Y = -60 through Y = 80**.
- Bedrock occupies the bottom boundary at Y = -60 and cannot be mined or replaced.
- The generator should create terrain above and below sea level, caves underground, and depth-weighted ore veins.
- World metadata must record the seed and generation version so a saved world can be reopened consistently.
- World creation, listing, loading, saving, and error handling must be verified against the Nintendo DS filesystem and existing map renderer before replacing the legacy world format.

## Colored blocks and panes

The target palette contains the 16 classic dye colors: white, orange, magenta, light blue, yellow, lime, pink, gray, light gray, cyan, purple, blue, brown, green, red, and black.

Provide all 16 colors for **wool**, **beds**, **stained glass**, and **stained glass panes**, plus **clear glass** and **clear glass panes**. Panes should be thin, connect visually to neighboring panes and glass blocks where practical, and use a lower-profile collision shape than full blocks. Beds should behave as placeable two-block structures rather than ordinary single cubes. Glass and panes should use transparent rendering if the existing DS renderer can support it within its memory budget.

## Compatibility and implementation notes

- Preserve support for existing legacy .world files where practical; do not silently overwrite or reinterpret them as the new format.
- Keep the renderer's current block-ID and texture-atlas limits in mind. Adding palette entries requires coordinated block definitions, texture mapping, interaction/drop rules, collision/rendering behavior, and save compatibility—not just adding names to a list.
- Validate generated worlds on emulator software, including the world-list screen, terrain rendering, player collision, saving, and reopening.
