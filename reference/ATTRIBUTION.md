# Attribution and licensing for `reference/`

Everything in this folder is **third-party work, mirrored for private design study**
on 2026-09-11. None of it is ours and none of it ships in any Agent City build without
its own licence check first. This repo is private; that is part of why this is a
reasonable place to keep them.

---

## Mirrored here

| Folder | Upstream | Licence | Notes |
|:--|:--|:--|:--|
| `pixel-agents/` | [pixel-agents-hq/pixel-agents](https://github.com/pixel-agents-hq/pixel-agents) | **MIT**, Copyright (c) 2026 Pablo De Lucca | Assets appear to be the project's own work, bundled under the repo licence. Cleanest provenance of anything here |
| `agent-town/` | [rafapetter/agent-town](https://github.com/rafapetter/agent-town) | Repo licence; screenshots are the project's own documentation images | Screenshots only, no code or sprites |
| `ai-town/` | [a16z-infra/ai-town](https://github.com/a16z-infra/ai-town) | MIT for the code. **Art is third-party, credited upstream** | Upstream credits: [16x16 game assets by George Bailey](https://opengameart.org/content/16x16-game-assets), [16x16 RPG tileset by hilau](https://opengameart.org/content/16x16-rpg-tileset), [Tiny RPG Forest by ansimuz](https://opengameart.org/content/tiny-rpg-forest) (all OpenGameArt), and UI from [Mounir Tohami](https://mounirtohami.itch.io/pixel-art-gui-elements). Check each OpenGameArt entry's own CC0/CC-BY terms before reuse |
| `generative-agents/` | [joonspk-research/generative_agents](https://github.com/joonspk-research/generative_agents) | Apache 2.0 for the code; cover image is the project's own | Character sprite provenance upstream is unclear - study only |
| `code-city/` | [wettel.github.io/codecity.html](https://wettel.github.io/codecity.html) and [gource.io](https://gource.io/) | Screenshots from the projects' own public pages | Academic and project promotional images, used here as design reference |

---

## Deliberately NOT mirrored

Two commercial packs are bundled inside the upstream repositories. They were found
during the download and excluded on purpose.

| Pack | Where it was found | Why excluded |
|:--|:--|:--|
| **Cute RPG World** (RPG Maker MV) | `generative_agents` → `the_ville/visuals/map_assets/Cute RPG World 40 usd packet/` - the folder name states the price | A paid pack, redistributed upstream with the price in the path. Not ours to copy. (It also blew past the Windows `MAX_PATH` limit on checkout, which is how it was noticed) |
| **`Modern.png`** (5.6 MB) | `ai-town` → `src/editor/tilesets/Modern.png` | The single largest art file in that repo and **not listed in AI Town's own credits block**, unlike every other tileset there. Consistent with a commercial "Modern Interiors / Exteriors"-family pack. Unverified provenance, so excluded |

If Agent City ever wants tiles at that quality, they get **bought**, not copied. Given
the design direction is flat untextured geometry in the CodeCity mould, it very likely
never needs them.

---

## Rules for this folder

1. **Reference only.** Nothing in `reference/` is imported by Agent City code. Keep it
   that way; if an asset is genuinely needed, copy it deliberately into an `assets/`
   folder of our own and record the licence there.
2. **Do not re-publish.** This repo stays private. If any part of Agent City is ever
   made public, `reference/` does not go with it.
3. **Re-check before reuse.** MIT on a repo does not mean MIT on the art inside it.
   AI Town is the live example: MIT code, third-party art, one uncredited file.
