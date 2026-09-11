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

<img width="100%" src="pixel-agents/Screenshot.jpg" alt="pixel-agents office"/>

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

<img width="100%" src="agent-town/playground-town.png" alt="agent-town kanban town"/>

The map is **state**. Position means something - it means task status. That is a real
idea and much stronger than map-as-office, even though the repo has 5 stars. Seven
themed skins of the same mechanic ship with it: town, office, farm, pirate ship,
rocket, space station.

<p>
<img src="agent-town/playground-office.png" width="32%" alt="office"/>
<img src="agent-town/playground-farm.png" width="32%" alt="farm"/>
<img src="agent-town/playground-pirate-ship.png" width="32%" alt="pirate ship"/>
</p>

### 3. Map-as-codebase - `code-city/`

`codecity-screenshot.png` is the one to look at, and it is the closest thing to what
Agent City should be. True isometric. Grey plates as districts, laid out as a flat
plane you look down on at an angle. Buildings extruded as plain boxes in blue, grey
and near-black - colour and height carry metrics, nothing is textured, nothing is
decorative. It reads instantly as a city and yet every pixel is data.

<img width="100%" src="code-city/codecity-screenshot.png" alt="CodeCity — the target look"/>

<p>
<img src="code-city/wof/jdk.png" width="32%" alt="JDK 1.5"/>
<img src="jscity/cities/angular.png" width="32%" alt="JSCity AngularJS"/>
<img src="code-city/gource-linux.jpg" width="32%" alt="Gource"/>
</p>

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

Sorted by upstream GitHub stars. Open these first.

| Folder | Stars | What is in it | Worth opening |
|:--|--:|:--|:--|
| `generative-agents/` | 22,087 | Smallville cover, 25 character sheets, speech bubbles, `the_ville_collision.png` (the actual town map), interior/house/grassland tiles (`map_assets/v1`–`v3`) | **`the_ville_collision.png`** - this is Smallville |
| `gource/` | 13,138 | `beam.png`, `file.png`, `user.png` sprites | With the stills in `code-city/gource-*.jpg` |
| `ai-town/` | 10,473 | Runtime tilesets, editor spritesheets, UI SVGs, animation JSON | `tilesets/magecity.png`, then `spritesheets/peeps.png` |
| `pixel-agents/` | 9,243 | Full bundled asset set: 6 character sheets, 9 floors, furniture each with `manifest.json`, pets, bubble sprites | `Screenshot.jpg` first, then any `furniture/*/manifest.json` |
| `3d-city/` | 1,744 | Preview stills + building/town/tile textures | `img/preview02.jpg` |
| `jscity/` | 1,400 | 60 city stills from the project wiki (Angular, jQuery, React, three.js, …) | **`cities/angular.png`** |
| `agent-office/` | 265 | Own character sprites (`char_0`–`char_5`, `characters.png`) | `characters.png` |
| `city-tour/` | 88 | `city_tour.gif` | The gif |
| `agent-town/` | 5 | 11 screenshots: 7 themed playgrounds + 4 dashboard views | `playground-town.png` |
| `code-city/` | — | CodeCity screenshot, ATED prize still, Gource stills, **Wall of Fame** (JDK, ArgoUML, JHotDraw, Vuze, Moose, Jmol) | **`codecity-screenshot.png` - this is the target look**, then `wof/jdk.png` |

---

## Not mirrored on purpose

Two commercial asset packs are bundled inside the upstream repos. They are documented
in [ATTRIBUTION.md](ATTRIBUTION.md) and deliberately left out of this folder. If the
project ever needs tiles of that quality, they get bought, not copied.
