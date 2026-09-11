# Reference assets - what the competition actually looks like

Downloaded 2026-09-11 so design decisions are made against real pixels instead of
descriptions. **Nothing here is ours.** Licences and what was deliberately *not*
mirrored are in [ATTRIBUTION.md](ATTRIBUTION.md).

---

## The three design patterns, and they are genuinely different

Looking at these side by side, the field is not one idea with variations. It is three.

### 1. Map-as-office - `pixel-agents/`

**Top-down, not isometric.** A Stardew-style floor plan: desks with monitors,
bookshelves, a kitchen, a lounge with armchairs, plants, dark navy void around the
building edge. Characters stand at desks and animate by activity - typing when
editing, reading when searching.

The map is **furniture**. It carries no information about the code. Move a desk and
nothing changes about what you learn. The signal is entirely in the characters.

This is the 9.2k-star one, and its charm is real, but note what it gives up: you
cannot tell from the picture *which project* is being worked on or *what shape* it is.

### 2. Map-as-workflow - `agent-town/`

The surprise of the survey. Its "town" is a **kanban board rendered as terrain** -
`Backlog`, `To Do`, `In Progress`, `Review`, `Done` are fenced zones with the count
painted on the ground (17, 12), and named agents (Claude, Nova, Atlas, Sage, Echo,
Pixel, Luna, Bolt, Cosmo, Ivy, Aria) physically stand in the zone matching their task
state, with `Chatting...` / `Discussing...` speech bubbles overhead.

The map is **state**. Position means something - it means task status. That is a real
idea and much stronger than map-as-office, even though the repo has 5 stars. Seven
themed skins of the same mechanic ship with it: town, office, farm, pirate ship,
rocket, space station.

### 3. Map-as-codebase - `code-city/`

`codecity-screenshot.png` is the one to look at, and it is the closest thing to what
Agent City should be. True isometric. Grey plates as districts, laid out as a flat
plane you look down on at an angle. Buildings extruded as plain boxes in blue, grey
and near-black - colour and height carry metrics, nothing is textured, nothing is
decorative. It reads instantly as a city and yet every pixel is data.

`gource-*.jpg` is the other half of this camp: the time axis, done right, since 2009.

**The map is the code.** Which is the whole point, and which is exactly what camps 1
and 2 do not have.

---

## What this settles for our design

- **Camera: take CodeCity's, not pixel-agents'.** Isometric with extruded boxes beats
  top-down floor plan, because the terrain has to mean something.
- **Citizens: take pixel-agents'.** The activity-driven character animation is the bit
  that makes it feel alive, and their sprite work is MIT.
- **Steal agent-town's insight that position encodes state.** Our districts encode
  *which project*; there is room to let a citizen's position within a district encode
  *what phase* the work is in.
- **Flat colour, no texture.** CodeCity is 2008 and still reads better than most of
  the modern pixel work, because it never decorates. That matches the house rule
  already: if it moves or it is coloured, it is carrying data.

---

## Folder map

| Folder | What is in it | Worth opening |
|:--|:--|:--|
| `pixel-agents/` | The full bundled asset set: `assets/characters/` (6 sheets), `floors/` (9), `carpets/`, `walls/`, `furniture/` (each with a `manifest.json` describing sprites, rotation groups, state groups, animation frames), plus `office.png`, `characters.png`, `banner.png` | `Screenshot.jpg` first, then any `furniture/*/manifest.json` - that manifest format is a solved problem worth copying |
| `agent-town/` | 11 screenshots: 7 themed playgrounds + 4 dashboard views (agents, analytics, kanban, timeline) | `playground-town.png`, then `playground-office.png` to see the same mechanic reskinned |
| `ai-town/` | `public-assets/` runtime tilesets and spritesheets, `spritesheets/` editor sheets, `tilesets/` (gentle, forest, magecity, Serene), `background.webp` | The spritesheets, for how they cut character motion frames |
| `generative-agents/` | `smallville-cover.png` (the 2023 paper's cover image) and `characters/` sprite sheets | The cover, for the aesthetic that started all of this |
| `code-city/` | `codecity-screenshot.png`, `codecity-ated-ict-2008.png`, `gource-linux.jpg`, `gource-papervision.jpg`, `gource-git.jpg` | **`codecity-screenshot.png` - this is the target look** |

---

## Not mirrored on purpose

Two commercial asset packs are bundled inside the upstream repos. They are documented
in [ATTRIBUTION.md](ATTRIBUTION.md) and deliberately left out of this folder. If the
project ever needs tiles of that quality, they get bought, not copied.
