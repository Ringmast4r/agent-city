<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:000000,100:A21CAF&height=220&section=header&text=AGENT%20CITY&fontSize=58&fontColor=ffffff&animation=twinkling&fontAlignY=35&desc=Your%20Claude%20Code%20sessions%2C%20rendered%20as%20a%20living%20city&descSize=18&descAlignY=58"/>

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1000&color=D946EF&center=true&vCenter=true&multiline=true&repeat=true&width=950&height=80&lines=Districts+are+projects.+Buildings+are+files.;Citizens+are+real+tool+calls%2C+not+a+simulation.;1%2C553+sessions+on+disk%2C+waiting+to+be+replayed.)](https://git.io/typing-svg)

<br>

[![Status](https://img.shields.io/badge/Status-Idea_stage-A21CAF?style=for-the-badge&logo=target&logoColor=white)](#-what_is_this)
[![Corpus](https://img.shields.io/badge/Corpus-1%2C553_sessions_%7C_2.5_GB-D946EF?style=for-the-badge&logo=databricks&logoColor=white)](#-data_sources)
[![Renderer](https://img.shields.io/badge/Renderer-Three.js_planned-000000?style=for-the-badge&logo=threedotjs&logoColor=white)](https://threejs.org/)
[![Prior art](https://img.shields.io/badge/Prior_art-15_projects_surveyed-A21CAF?style=for-the-badge&logo=github&logoColor=white)](#-prior_art)

[![Stars](https://img.shields.io/github/stars/Ringmast4r/agent-city?style=flat-square&color=A21CAF&label=%E2%98%85%20Stars)](https://github.com/Ringmast4r/agent-city/stargazers)
[![Forks](https://img.shields.io/github/forks/Ringmast4r/agent-city?style=flat-square&color=D946EF&label=%E2%9A%A1%20Forks)](https://github.com/Ringmast4r/agent-city/network/members)
[![Repo Size](https://img.shields.io/github/repo-size/Ringmast4r/agent-city?style=flat-square&color=000000)](#)
[![Last Commit](https://img.shields.io/github/last-commit/Ringmast4r/agent-city?style=flat-square&color=A21CAF)](https://github.com/Ringmast4r/agent-city/commits/main)
[![Visitors](https://visitor-badge.laobi.icu/badge?page_id=Ringmast4r.agent-city)](#)

</div>

---

## `> what_is_this`

```bash
you@github:~$ cat project.txt

  PURPOSE:        render my own Claude Code sessions as an isometric city
  DISTRICTS:      the numbered D: libraries (00 Database ... 27 Chrome Ext)
  BUILDINGS:      real files - height = LOC, footprint = size
  CITIZENS:       real tool calls and subagents, read from transcripts
  CORPUS:         1,553 sessions | 2.5 GB | biggest session 17,256 lines
  STATUS:         [ IDEA STAGE - NOTHING BUILT YET ]
```

> **The city is not a simulation, it is a read-out.** Every person on screen is an
> actual tool call that actually happened, in an actual file, at an actual timestamp.

Full design doc: **[IDEA.md](IDEA.md)**. Competitor assets and what they look like:
**[reference/](reference/README.md)**.

---

## `> is_it_possible`

Yes, and it is less speculative than it sounds. Every individually risky piece is
already shipping in someone else's project. Nothing here needs inventing - it needs
combining.

| Risky-sounding piece | Already proven by | Verdict |
|:--|:--|:--|
| Reading agent activity out of Claude Code live | `pixel-agents`, 9,243 stars | Solved, two ways |
| Parsing a multi-GB `~/.claude/projects` corpus | `token-dashboard` - Python stdlib + SQLite, 20-60 s full scan | Solved, at this exact scale |
| Turning a file tree into a 3D city in a browser | `JSCity` (three.js) | Solved |
| Animating repo history over a time axis | `Gource`, since 2009 | Solved |
| Little people walking around doing agent work | `pixel-agents`, `agent-town`, `AI Town` | Solved |

**What nobody has done is join them.** The field splits into three camps that have
never met - see [reference/README.md](reference/README.md) for the screenshots that
make this obvious:

| Camp | Example | The map means... |
|:--|:--|:--|
| Map-as-office | `pixel-agents` | Nothing. It is furniture. All signal is in the characters |
| Map-as-workflow | `agent-town` | Task state - agents stand in `Backlog` / `In Progress` / `Done` zones |
| Map-as-codebase | `CodeCity`, `JSCity` | The code itself - but static, empty, no clock and no people |

Agent City is the join: **real terrain from the actual file tree, walked by real
citizens from actual tool calls, over a real time axis** - plus the thing nobody else
has at all, a back catalogue of 1,553 sessions to replay as a chronicle.

The three camps, in pixels:

<p>
<img src="reference/pixel-agents/Screenshot.jpg" width="32%" alt="pixel-agents — map is furniture"/>
<img src="reference/agent-town/playground-town.png" width="32%" alt="agent-town — map is task state"/>
<img src="reference/code-city/codecity-screenshot.png" width="32%" alt="CodeCity — map is the code"/>
</p>

---

## `> prior_art`

Surveyed 2026-09-11, **sorted by GitHub stars**. Screenshots and sprites are under [`reference/`](reference/README.md) so you can see what each one actually looks like.

### Agent-as-citizen (the people)

| Project | Stars | Stack | How it knows what the agent is doing |
|:--|--:|:--|:--|
| **[Generative Agents](https://github.com/joonspk-research/generative_agents)** * | **22,087** | Python + Django, Phaser frontend (Smallville) | Simulated. The 2023 paper that started the aesthetic |
| **[AI Town](https://github.com/a16z-infra/ai-town)** * | **10,473** | **PixiJS + pixi-react**, **Convex** (db + serverless + vector search), Clerk, Fly.io | Simulated. 60 ticks/s bundled into one DB step/s; clients replay "historical objects" for smooth motion between sparse writes |
| **[pixel-agents](https://github.com/pixel-agents-hq/pixel-agents)** * | **9,243** | TypeScript, React 19 + Vite, **Canvas 2D**, Fastify, Node 20+, esbuild, Vitest + Playwright | **Real telemetry.** Claude Code **hooks primary** (`SessionStart`, `PreToolUse`, `PermissionRequest`, `Stop`) with a **JSONL fallback** over `~/.claude/projects/`. Both normalise into one `AgentEvent` model behind a typed `HookProvider` interface |
| [agent-office](https://github.com/harishkotra/agent-office) * | 265 | Phaser.js, Colyseus, React, SQLite, Ollama | Simulated - a think loop every ~15 s. SQLite memories with embedding + cosine recall |
| [agent-town](https://github.com/rafapetter/agent-town) * | 5 | Pure TypeScript, **zero dependencies**, Canvas 2D, procedural pixel art | Direct TS API (`addAgent`, `updateAgent`, `logActivity`) plus a WebSocket bridge for Claude Code / Cursor / Codex |

### Code-as-city (the buildings)

| Project | Stars | Stack | Mapping |
|:--|--:|:--|:--|
| **[Gource](https://github.com/acaudwell/gource)** * | **13,138** | C++, OpenGL/SDL | Repo history as an animated tree, committers as avatars. The time axis done right |
| **[3d.city](https://github.com/lo-th/3d.city)** * | **1,744** | three.js, WebGL2/WebGPU | Procedural city builder - layout, camera, textured blocks |
| **[JSCity](https://github.com/aserg-ufmg/JSCity)** * | **1,400** | **three.js** | Folders are districts, files are sub-districts, **buildings are functions**; height = LOC, base = variable count |
| [city-tour](https://github.com/jstrait/city-tour) * | 88 | three.js, WebGL | Procedural city generation - layout and camera reference |
| [CodeCity](https://wettel.github.io/codecity.html) * (Wettel, 2008) | — | VisualWorks Smalltalk on Moose, OpenGL | Packages are districts, classes are buildings, methods are floors. **The target look.** No GitHub repo; academic original |

### Claude Code transcript tooling (the data pipeline)

| Project | Stars | Stack | Notes |
|:--|--:|:--|:--|
| [claude-code-transcripts](https://github.com/simonw/claude-code-transcripts) | **1,686** | Python | JSONL to paginated static HTML |
| [claude-code-log](https://github.com/daaain/claude-code-log) | 1,213 | Python CLI | JSONL to HTML / Markdown |
| **[token-dashboard](https://github.com/nateherkai/token-dashboard)** | 694 | **Python 3 stdlib only**, **SQLite**, vanilla JS + ECharts, **no build step** | Scans `~/.claude/projects/`, dedupes by `message.id`, **20-60 s full initial scan on a heavy machine**, re-scan every 30 s over SSE. Tool and file heatmaps |
| [ClaudeCodeJSONLParser](https://github.com/amac0/ClaudeCodeJSONLParser) | 20 | HTML tool | JSONL events and git history on one timeline - closest to the chronicle idea |

---

## `> look`

Every visual file under `reference/` is embedded below — **350 images**, highest stars first.

| Project | Stars | Images |
|:--|--:|--:|
| [Generative Agents](#generative-agents) | 22,087 | 99 |
| [Gource](#gource) | 13,138 | 3 |
| [AI Town](#ai-town) | 10,473 | 57 |
| [pixel-agents](#pixel-agents) | 9,243 | 64 |
| [3d.city](#3dcity) | 1,744 | 15 |
| [JSCity](#jscity) | 1,400 | 80 |
| [agent-office](#agent-office) | 265 | 7 |
| [city-tour](#city-tour) | 88 | 2 |
| [agent-town](#agent-town) | 5 | 11 |
| [CodeCity](#codecity) | — | 12 |

### Generative Agents

[Generative Agents](https://github.com/joonspk-research/generative_agents) — **22,087 ★** — `99` files in `reference/generative-agents/`

**`cover.png`**

<img width="100%" src="reference/generative-agents/cover.png" alt="cover.png"/>

**`smallville-cover.png`**

<img width="100%" src="reference/generative-agents/smallville-cover.png" alt="smallville-cover.png"/>

**`the_ville2.png`**

<img width="100%" src="reference/generative-agents/the_ville2.png" alt="the_ville2.png"/>

**`the_ville_collision.png`**

<img width="100%" src="reference/generative-agents/the_ville_collision.png" alt="the_ville_collision.png"/>

<p>
<img src="reference/generative-agents/atlas.png" width="16%" alt="atlas.png" title="atlas.png"/>
</p>

#### `generative-agents/characters`

<p>
<img src="reference/generative-agents/characters/Abigail_Chen.png" width="16%" alt="Abigail_Chen.png" title="Abigail_Chen.png"/><img src="reference/generative-agents/characters/Adam_Smith.png" width="16%" alt="Adam_Smith.png" title="Adam_Smith.png"/><img src="reference/generative-agents/characters/Arthur_Burton.png" width="16%" alt="Arthur_Burton.png" title="Arthur_Burton.png"/><img src="reference/generative-agents/characters/Ayesha_Khan.png" width="16%" alt="Ayesha_Khan.png" title="Ayesha_Khan.png"/><img src="reference/generative-agents/characters/Carlos_Gomez.png" width="16%" alt="Carlos_Gomez.png" title="Carlos_Gomez.png"/><img src="reference/generative-agents/characters/Carmen_Ortiz.png" width="16%" alt="Carmen_Ortiz.png" title="Carmen_Ortiz.png"/><img src="reference/generative-agents/characters/Eddy_Lin.png" width="16%" alt="Eddy_Lin.png" title="Eddy_Lin.png"/><img src="reference/generative-agents/characters/Francisco_Lopez.png" width="16%" alt="Francisco_Lopez.png" title="Francisco_Lopez.png"/><img src="reference/generative-agents/characters/Giorgio_Rossi.png" width="16%" alt="Giorgio_Rossi.png" title="Giorgio_Rossi.png"/><img src="reference/generative-agents/characters/Hailey_Johnson.png" width="16%" alt="Hailey_Johnson.png" title="Hailey_Johnson.png"/><img src="reference/generative-agents/characters/Isabella_Rodriguez.png" width="16%" alt="Isabella_Rodriguez.png" title="Isabella_Rodriguez.png"/><img src="reference/generative-agents/characters/Jane_Moreno.png" width="16%" alt="Jane_Moreno.png" title="Jane_Moreno.png"/><img src="reference/generative-agents/characters/Jennifer_Moore.png" width="16%" alt="Jennifer_Moore.png" title="Jennifer_Moore.png"/><img src="reference/generative-agents/characters/John_Lin.png" width="16%" alt="John_Lin.png" title="John_Lin.png"/><img src="reference/generative-agents/characters/Klaus_Mueller.png" width="16%" alt="Klaus_Mueller.png" title="Klaus_Mueller.png"/><img src="reference/generative-agents/characters/Latoya_Williams.png" width="16%" alt="Latoya_Williams.png" title="Latoya_Williams.png"/><img src="reference/generative-agents/characters/Maria_Lopez.png" width="16%" alt="Maria_Lopez.png" title="Maria_Lopez.png"/><img src="reference/generative-agents/characters/Mei_Lin.png" width="16%" alt="Mei_Lin.png" title="Mei_Lin.png"/><img src="reference/generative-agents/characters/Rajiv_Patel.png" width="16%" alt="Rajiv_Patel.png" title="Rajiv_Patel.png"/><img src="reference/generative-agents/characters/Ryan_Park.png" width="16%" alt="Ryan_Park.png" title="Ryan_Park.png"/><img src="reference/generative-agents/characters/Sam_Moore.png" width="16%" alt="Sam_Moore.png" title="Sam_Moore.png"/><img src="reference/generative-agents/characters/Tamara_Taylor.png" width="16%" alt="Tamara_Taylor.png" title="Tamara_Taylor.png"/><img src="reference/generative-agents/characters/Tom_Moreno.png" width="16%" alt="Tom_Moreno.png" title="Tom_Moreno.png"/><img src="reference/generative-agents/characters/Wolfgang_Schulz.png" width="16%" alt="Wolfgang_Schulz.png" title="Wolfgang_Schulz.png"/><img src="reference/generative-agents/characters/Yuriko_Yamamoto.png" width="16%" alt="Yuriko_Yamamoto.png" title="Yuriko_Yamamoto.png"/>
</p>

#### `generative-agents/characters/original`

<p>
<img src="reference/generative-agents/characters/original/Abigail_Chen.png" width="16%" alt="Abigail_Chen.png" title="Abigail_Chen.png"/><img src="reference/generative-agents/characters/original/Adam_Smith.png" width="16%" alt="Adam_Smith.png" title="Adam_Smith.png"/><img src="reference/generative-agents/characters/original/Arthur_Burton.png" width="16%" alt="Arthur_Burton.png" title="Arthur_Burton.png"/><img src="reference/generative-agents/characters/original/Ayesha_Khan.png" width="16%" alt="Ayesha_Khan.png" title="Ayesha_Khan.png"/><img src="reference/generative-agents/characters/original/Carlos_Gomez.png" width="16%" alt="Carlos_Gomez.png" title="Carlos_Gomez.png"/><img src="reference/generative-agents/characters/original/Carmen_Ortiz.png" width="16%" alt="Carmen_Ortiz.png" title="Carmen_Ortiz.png"/><img src="reference/generative-agents/characters/original/Eddy_Lin.png" width="16%" alt="Eddy_Lin.png" title="Eddy_Lin.png"/><img src="reference/generative-agents/characters/original/Francisco_Lopez.png" width="16%" alt="Francisco_Lopez.png" title="Francisco_Lopez.png"/><img src="reference/generative-agents/characters/original/Giorgio_Rossi.png" width="16%" alt="Giorgio_Rossi.png" title="Giorgio_Rossi.png"/><img src="reference/generative-agents/characters/original/Hailey_Johnson.png" width="16%" alt="Hailey_Johnson.png" title="Hailey_Johnson.png"/><img src="reference/generative-agents/characters/original/Isabella_Rodriguez.png" width="16%" alt="Isabella_Rodriguez.png" title="Isabella_Rodriguez.png"/><img src="reference/generative-agents/characters/original/Jane_Moreno.png" width="16%" alt="Jane_Moreno.png" title="Jane_Moreno.png"/><img src="reference/generative-agents/characters/original/Jennifer_Moore.png" width="16%" alt="Jennifer_Moore.png" title="Jennifer_Moore.png"/><img src="reference/generative-agents/characters/original/John_Lin.png" width="16%" alt="John_Lin.png" title="John_Lin.png"/><img src="reference/generative-agents/characters/original/Klaus_Mueller.png" width="16%" alt="Klaus_Mueller.png" title="Klaus_Mueller.png"/><img src="reference/generative-agents/characters/original/Latoya_Williams.png" width="16%" alt="Latoya_Williams.png" title="Latoya_Williams.png"/><img src="reference/generative-agents/characters/original/Maria_Lopez.png" width="16%" alt="Maria_Lopez.png" title="Maria_Lopez.png"/><img src="reference/generative-agents/characters/original/Mei_Lin.png" width="16%" alt="Mei_Lin.png" title="Mei_Lin.png"/><img src="reference/generative-agents/characters/original/Rajiv_Patel.png" width="16%" alt="Rajiv_Patel.png" title="Rajiv_Patel.png"/><img src="reference/generative-agents/characters/original/Ryan_Park.png" width="16%" alt="Ryan_Park.png" title="Ryan_Park.png"/><img src="reference/generative-agents/characters/original/Sam_Moore.png" width="16%" alt="Sam_Moore.png" title="Sam_Moore.png"/><img src="reference/generative-agents/characters/original/Tamara_Taylor.png" width="16%" alt="Tamara_Taylor.png" title="Tamara_Taylor.png"/><img src="reference/generative-agents/characters/original/Tom_Moreno.png" width="16%" alt="Tom_Moreno.png" title="Tom_Moreno.png"/><img src="reference/generative-agents/characters/original/Wolfgang_Schulz.png" width="16%" alt="Wolfgang_Schulz.png" title="Wolfgang_Schulz.png"/><img src="reference/generative-agents/characters/original/Yuriko_Yamamoto.png" width="16%" alt="Yuriko_Yamamoto.png" title="Yuriko_Yamamoto.png"/>
</p>

#### `generative-agents/characters/profile`

<p>
<img src="reference/generative-agents/characters/profile/Abigail_Chen.png" width="16%" alt="Abigail_Chen.png" title="Abigail_Chen.png"/><img src="reference/generative-agents/characters/profile/Adam_Smith.png" width="16%" alt="Adam_Smith.png" title="Adam_Smith.png"/><img src="reference/generative-agents/characters/profile/Arthur_Burton.png" width="16%" alt="Arthur_Burton.png" title="Arthur_Burton.png"/><img src="reference/generative-agents/characters/profile/Ayesha_Khan.png" width="16%" alt="Ayesha_Khan.png" title="Ayesha_Khan.png"/><img src="reference/generative-agents/characters/profile/Carlos_Gomez.png" width="16%" alt="Carlos_Gomez.png" title="Carlos_Gomez.png"/><img src="reference/generative-agents/characters/profile/Carmen_Ortiz.png" width="16%" alt="Carmen_Ortiz.png" title="Carmen_Ortiz.png"/><img src="reference/generative-agents/characters/profile/Eddy_Lin.png" width="16%" alt="Eddy_Lin.png" title="Eddy_Lin.png"/><img src="reference/generative-agents/characters/profile/Francisco_Lopez.png" width="16%" alt="Francisco_Lopez.png" title="Francisco_Lopez.png"/><img src="reference/generative-agents/characters/profile/Giorgio_Rossi.png" width="16%" alt="Giorgio_Rossi.png" title="Giorgio_Rossi.png"/><img src="reference/generative-agents/characters/profile/Hailey_Johnson.png" width="16%" alt="Hailey_Johnson.png" title="Hailey_Johnson.png"/><img src="reference/generative-agents/characters/profile/Isabella_Rodriguez.png" width="16%" alt="Isabella_Rodriguez.png" title="Isabella_Rodriguez.png"/><img src="reference/generative-agents/characters/profile/Jane_Moreno.png" width="16%" alt="Jane_Moreno.png" title="Jane_Moreno.png"/><img src="reference/generative-agents/characters/profile/Jennifer_Moore.png" width="16%" alt="Jennifer_Moore.png" title="Jennifer_Moore.png"/><img src="reference/generative-agents/characters/profile/John_Lin.png" width="16%" alt="John_Lin.png" title="John_Lin.png"/><img src="reference/generative-agents/characters/profile/Klaus_Mueller.png" width="16%" alt="Klaus_Mueller.png" title="Klaus_Mueller.png"/><img src="reference/generative-agents/characters/profile/Latoya_Williams.png" width="16%" alt="Latoya_Williams.png" title="Latoya_Williams.png"/><img src="reference/generative-agents/characters/profile/Maria_Lopez.png" width="16%" alt="Maria_Lopez.png" title="Maria_Lopez.png"/><img src="reference/generative-agents/characters/profile/Mei_Lin.png" width="16%" alt="Mei_Lin.png" title="Mei_Lin.png"/><img src="reference/generative-agents/characters/profile/Rajiv_Patel.png" width="16%" alt="Rajiv_Patel.png" title="Rajiv_Patel.png"/><img src="reference/generative-agents/characters/profile/Ryan_Park.png" width="16%" alt="Ryan_Park.png" title="Ryan_Park.png"/><img src="reference/generative-agents/characters/profile/Sam_Moore.png" width="16%" alt="Sam_Moore.png" title="Sam_Moore.png"/><img src="reference/generative-agents/characters/profile/Tamara_Taylor.png" width="16%" alt="Tamara_Taylor.png" title="Tamara_Taylor.png"/><img src="reference/generative-agents/characters/profile/Tom_Moreno.png" width="16%" alt="Tom_Moreno.png" title="Tom_Moreno.png"/><img src="reference/generative-agents/characters/profile/Wolfgang_Schulz.png" width="16%" alt="Wolfgang_Schulz.png" title="Wolfgang_Schulz.png"/><img src="reference/generative-agents/characters/profile/Yuriko_Yamamoto.png" width="16%" alt="Yuriko_Yamamoto.png" title="Yuriko_Yamamoto.png"/>
</p>

#### `generative-agents/map_assets/v1`

**`Interiors_32x32_full.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/Interiors_32x32_full.png" alt="Interiors_32x32_full.png"/>

**`interiors_pt1.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/interiors_pt1.png" alt="interiors_pt1.png"/>

**`interiors_pt2.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/interiors_pt2.png" alt="interiors_pt2.png"/>

**`interiors_pt3.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/interiors_pt3.png" alt="interiors_pt3.png"/>

**`interiors_pt4.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/interiors_pt4.png" alt="interiors_pt4.png"/>

**`interiors_pt5.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/interiors_pt5.png" alt="interiors_pt5.png"/>

**`Room_Builder_32x32.png`**

<img width="100%" src="reference/generative-agents/map_assets/v1/Room_Builder_32x32.png" alt="Room_Builder_32x32.png"/>

#### `generative-agents/map_assets/v2`

**`TopDownHouse_DoorsAndWindows.png`**

<img width="100%" src="reference/generative-agents/map_assets/v2/TopDownHouse_DoorsAndWindows.png" alt="TopDownHouse_DoorsAndWindows.png"/>

**`TopDownHouse_FloorsAndWalls.png`**

<img width="100%" src="reference/generative-agents/map_assets/v2/TopDownHouse_FloorsAndWalls.png" alt="TopDownHouse_FloorsAndWalls.png"/>

**`TopDownHouse_FurnitureState1.png`**

<img width="100%" src="reference/generative-agents/map_assets/v2/TopDownHouse_FurnitureState1.png" alt="TopDownHouse_FurnitureState1.png"/>

**`TopDownHouse_FurnitureState2.png`**

<img width="100%" src="reference/generative-agents/map_assets/v2/TopDownHouse_FurnitureState2.png" alt="TopDownHouse_FurnitureState2.png"/>

**`TopDownHouse_SmallItems.png`**

<img width="100%" src="reference/generative-agents/map_assets/v2/TopDownHouse_SmallItems.png" alt="TopDownHouse_SmallItems.png"/>

#### `generative-agents/map_assets/v3`

**`tileset-grassland-grass.png`**

<img width="100%" src="reference/generative-agents/map_assets/v3/tileset-grassland-grass.png" alt="tileset-grassland-grass.png"/>

**`tileset-grassland-paths.png`**

<img width="100%" src="reference/generative-agents/map_assets/v3/tileset-grassland-paths.png" alt="tileset-grassland-paths.png"/>

**`tileset-grassland-props.png`**

<img width="100%" src="reference/generative-agents/map_assets/v3/tileset-grassland-props.png" alt="tileset-grassland-props.png"/>

**`tileset-grassland-water.png`**

<img width="100%" src="reference/generative-agents/map_assets/v3/tileset-grassland-water.png" alt="tileset-grassland-water.png"/>

#### `generative-agents/speech_bubble`

<p>
<img src="reference/generative-agents/speech_bubble/v1.png" width="16%" alt="v1.png" title="v1.png"/><img src="reference/generative-agents/speech_bubble/v2.png" width="16%" alt="v2.png" title="v2.png"/><img src="reference/generative-agents/speech_bubble/v3.png" width="16%" alt="v3.png" title="v3.png"/>
</p>

---

### Gource

[Gource](https://github.com/acaudwell/Gource) — **13,138 ★** — `3` files in `reference/gource/`

<p>
<img src="reference/gource/beam.png" width="16%" alt="beam.png" title="beam.png"/><img src="reference/gource/file.png" width="16%" alt="file.png" title="file.png"/><img src="reference/gource/user.png" width="16%" alt="user.png" title="user.png"/>
</p>

---

### AI Town

[AI Town](https://github.com/a16z-infra/ai-town) — **10,473 ★** — `57` files in `reference/ai-town/`

**`background.webp`**

<img width="100%" src="reference/ai-town/background.webp" alt="background.webp"/>

#### `ai-town/editor`

**`campfire.png`**

<img width="100%" src="reference/ai-town/editor/campfire.png" alt="campfire.png"/>

**`doll.png`**

<img width="100%" src="reference/ai-town/editor/doll.png" alt="doll.png"/>

**`forest.png`**

<img width="100%" src="reference/ai-town/editor/forest.png" alt="forest.png"/>

**`gentle-obj.png`**

<img width="100%" src="reference/ai-town/editor/gentle-obj.png" alt="gentle-obj.png"/>

**`gentle.png`**

<img width="100%" src="reference/ai-town/editor/gentle.png" alt="gentle.png"/>

**`gentlesparkle32.png`**

<img width="100%" src="reference/ai-town/editor/gentlesparkle32.png" alt="gentlesparkle32.png"/>

**`gentlewaterfall32.png`**

<img width="100%" src="reference/ai-town/editor/gentlewaterfall32.png" alt="gentlewaterfall32.png"/>

**`magecity.png`**

<img width="100%" src="reference/ai-town/editor/magecity.png" alt="magecity.png"/>

**`peeps.png`**

<img width="100%" src="reference/ai-town/editor/peeps.png" alt="peeps.png"/>

**`phantasy2.png`**

<img width="100%" src="reference/ai-town/editor/phantasy2.png" alt="phantasy2.png"/>

**`Serene.png`**

<img width="100%" src="reference/ai-town/editor/Serene.png" alt="Serene.png"/>

**`tall.png`**

<img width="100%" src="reference/ai-town/editor/tall.png" alt="tall.png"/>

**`windmill.png`**

<img width="100%" src="reference/ai-town/editor/windmill.png" alt="windmill.png"/>

**`women.png`**

<img width="100%" src="reference/ai-town/editor/women.png" alt="women.png"/>

#### `ai-town/public-assets`

**`32x32folk.png`**

<img width="100%" src="reference/ai-town/public-assets/32x32folk.png" alt="32x32folk.png"/>

**`gentle-obj.png`**

<img width="100%" src="reference/ai-town/public-assets/gentle-obj.png" alt="gentle-obj.png"/>

**`heart-empty.png`**

<img width="100%" src="reference/ai-town/public-assets/heart-empty.png" alt="heart-empty.png"/>

**`magecity.png`**

<img width="100%" src="reference/ai-town/public-assets/magecity.png" alt="magecity.png"/>

**`player.png`**

<img width="100%" src="reference/ai-town/public-assets/player.png" alt="player.png"/>

**`rpg-tileset.png`**

<img width="100%" src="reference/ai-town/public-assets/rpg-tileset.png" alt="rpg-tileset.png"/>

#### `ai-town/public-assets/spritesheets`

**`campfire.png`**

<img width="100%" src="reference/ai-town/public-assets/spritesheets/campfire.png" alt="campfire.png"/>

**`gentlesparkle32.png`**

<img width="100%" src="reference/ai-town/public-assets/spritesheets/gentlesparkle32.png" alt="gentlesparkle32.png"/>

**`gentlewaterfall32.png`**

<img width="100%" src="reference/ai-town/public-assets/spritesheets/gentlewaterfall32.png" alt="gentlewaterfall32.png"/>

**`windmill.png`**

<img width="100%" src="reference/ai-town/public-assets/spritesheets/windmill.png" alt="windmill.png"/>

#### `ai-town/spritesheets`

**`campfire.png`**

<img width="100%" src="reference/ai-town/spritesheets/campfire.png" alt="campfire.png"/>

**`doll.png`**

<img width="100%" src="reference/ai-town/spritesheets/doll.png" alt="doll.png"/>

**`gentlesparkle32.png`**

<img width="100%" src="reference/ai-town/spritesheets/gentlesparkle32.png" alt="gentlesparkle32.png"/>

**`gentlewaterfall32.png`**

<img width="100%" src="reference/ai-town/spritesheets/gentlewaterfall32.png" alt="gentlewaterfall32.png"/>

**`peeps.png`**

<img width="100%" src="reference/ai-town/spritesheets/peeps.png" alt="peeps.png"/>

**`tall.png`**

<img width="100%" src="reference/ai-town/spritesheets/tall.png" alt="tall.png"/>

**`windmill.png`**

<img width="100%" src="reference/ai-town/spritesheets/windmill.png" alt="windmill.png"/>

**`women.png`**

<img width="100%" src="reference/ai-town/spritesheets/women.png" alt="women.png"/>

#### `ai-town/tilesets`

**`forest.png`**

<img width="100%" src="reference/ai-town/tilesets/forest.png" alt="forest.png"/>

**`gentle-obj.png`**

<img width="100%" src="reference/ai-town/tilesets/gentle-obj.png" alt="gentle-obj.png"/>

**`gentle.png`**

<img width="100%" src="reference/ai-town/tilesets/gentle.png" alt="gentle.png"/>

**`magecity.png`**

<img width="100%" src="reference/ai-town/tilesets/magecity.png" alt="magecity.png"/>

**`phantasy2.png`**

<img width="100%" src="reference/ai-town/tilesets/phantasy2.png" alt="phantasy2.png"/>

**`Serene.png`**

<img width="100%" src="reference/ai-town/tilesets/Serene.png" alt="Serene.png"/>

#### `ai-town/ui`

**`background.webp`**

<img width="100%" src="reference/ai-town/ui/background.webp" alt="background.webp"/>

<p>
<img src="reference/ai-town/ui/a16z.png" width="16%" alt="a16z.png" title="a16z.png"/><img src="reference/ai-town/ui/box.svg" width="16%" alt="box.svg" title="box.svg"/><img src="reference/ai-town/ui/bubble-left.svg" width="16%" alt="bubble-left.svg" title="bubble-left.svg"/><img src="reference/ai-town/ui/bubble-right.svg" width="16%" alt="bubble-right.svg" title="bubble-right.svg"/><img src="reference/ai-town/ui/button.svg" width="16%" alt="button.svg" title="button.svg"/><img src="reference/ai-town/ui/button_pressed.svg" width="16%" alt="button_pressed.svg" title="button_pressed.svg"/><img src="reference/ai-town/ui/chats.svg" width="16%" alt="chats.svg" title="chats.svg"/><img src="reference/ai-town/ui/close.svg" width="16%" alt="close.svg" title="close.svg"/><img src="reference/ai-town/ui/convex-bg.webp" width="16%" alt="convex-bg.webp" title="convex-bg.webp"/><img src="reference/ai-town/ui/convex.svg" width="16%" alt="convex.svg" title="convex.svg"/><img src="reference/ai-town/ui/desc.svg" width="16%" alt="desc.svg" title="desc.svg"/><img src="reference/ai-town/ui/frame.svg" width="16%" alt="frame.svg" title="frame.svg"/><img src="reference/ai-town/ui/help.svg" width="16%" alt="help.svg" title="help.svg"/><img src="reference/ai-town/ui/interact.svg" width="16%" alt="interact.svg" title="interact.svg"/><img src="reference/ai-town/ui/jewel_box.svg" width="16%" alt="jewel_box.svg" title="jewel_box.svg"/><img src="reference/ai-town/ui/star.svg" width="16%" alt="star.svg" title="star.svg"/><img src="reference/ai-town/ui/volume.svg" width="16%" alt="volume.svg" title="volume.svg"/>
</p>

---

### pixel-agents

[pixel-agents](https://github.com/pixel-agents-hq/pixel-agents) — **9,243 ★** — `64` files in `reference/pixel-agents/`

#### `pixel-agents/assets/carpets`

<p>
<img src="reference/pixel-agents/assets/carpets/carpet_0.png" width="16%" alt="carpet_0.png" title="carpet_0.png"/><img src="reference/pixel-agents/assets/carpets/carpet_1.png" width="16%" alt="carpet_1.png" title="carpet_1.png"/><img src="reference/pixel-agents/assets/carpets/carpet_2.png" width="16%" alt="carpet_2.png" title="carpet_2.png"/>
</p>

#### `pixel-agents/assets/characters`

<p>
<img src="reference/pixel-agents/assets/characters/char_0.png" width="16%" alt="char_0.png" title="char_0.png"/><img src="reference/pixel-agents/assets/characters/char_1.png" width="16%" alt="char_1.png" title="char_1.png"/><img src="reference/pixel-agents/assets/characters/char_2.png" width="16%" alt="char_2.png" title="char_2.png"/><img src="reference/pixel-agents/assets/characters/char_3.png" width="16%" alt="char_3.png" title="char_3.png"/><img src="reference/pixel-agents/assets/characters/char_4.png" width="16%" alt="char_4.png" title="char_4.png"/><img src="reference/pixel-agents/assets/characters/char_5.png" width="16%" alt="char_5.png" title="char_5.png"/>
</p>

#### `pixel-agents/assets/floors`

<p>
<img src="reference/pixel-agents/assets/floors/floor_0.png" width="16%" alt="floor_0.png" title="floor_0.png"/><img src="reference/pixel-agents/assets/floors/floor_1.png" width="16%" alt="floor_1.png" title="floor_1.png"/><img src="reference/pixel-agents/assets/floors/floor_2.png" width="16%" alt="floor_2.png" title="floor_2.png"/><img src="reference/pixel-agents/assets/floors/floor_3.png" width="16%" alt="floor_3.png" title="floor_3.png"/><img src="reference/pixel-agents/assets/floors/floor_4.png" width="16%" alt="floor_4.png" title="floor_4.png"/><img src="reference/pixel-agents/assets/floors/floor_5.png" width="16%" alt="floor_5.png" title="floor_5.png"/><img src="reference/pixel-agents/assets/floors/floor_6.png" width="16%" alt="floor_6.png" title="floor_6.png"/><img src="reference/pixel-agents/assets/floors/floor_7.png" width="16%" alt="floor_7.png" title="floor_7.png"/><img src="reference/pixel-agents/assets/floors/floor_8.png" width="16%" alt="floor_8.png" title="floor_8.png"/>
</p>

#### `pixel-agents/assets/furniture/BIN`

<p>
<img src="reference/pixel-agents/assets/furniture/BIN/BIN.png" width="16%" alt="BIN.png" title="BIN.png"/>
</p>

#### `pixel-agents/assets/furniture/BOOKSHELF`

<p>
<img src="reference/pixel-agents/assets/furniture/BOOKSHELF/BOOKSHELF.png" width="16%" alt="BOOKSHELF.png" title="BOOKSHELF.png"/>
</p>

#### `pixel-agents/assets/furniture/CACTUS`

<p>
<img src="reference/pixel-agents/assets/furniture/CACTUS/CACTUS.png" width="16%" alt="CACTUS.png" title="CACTUS.png"/>
</p>

#### `pixel-agents/assets/furniture/CLOCK`

<p>
<img src="reference/pixel-agents/assets/furniture/CLOCK/CLOCK.png" width="16%" alt="CLOCK.png" title="CLOCK.png"/>
</p>

#### `pixel-agents/assets/furniture/COFFEE`

<p>
<img src="reference/pixel-agents/assets/furniture/COFFEE/COFFEE.png" width="16%" alt="COFFEE.png" title="COFFEE.png"/>
</p>

#### `pixel-agents/assets/furniture/COFFEE_TABLE`

<p>
<img src="reference/pixel-agents/assets/furniture/COFFEE_TABLE/COFFEE_TABLE.png" width="16%" alt="COFFEE_TABLE.png" title="COFFEE_TABLE.png"/>
</p>

#### `pixel-agents/assets/furniture/CUSHIONED_BENCH`

<p>
<img src="reference/pixel-agents/assets/furniture/CUSHIONED_BENCH/CUSHIONED_BENCH.png" width="16%" alt="CUSHIONED_BENCH.png" title="CUSHIONED_BENCH.png"/>
</p>

#### `pixel-agents/assets/furniture/CUSHIONED_CHAIR`

<p>
<img src="reference/pixel-agents/assets/furniture/CUSHIONED_CHAIR/CUSHIONED_CHAIR_BACK.png" width="16%" alt="CUSHIONED_CHAIR_BACK.png" title="CUSHIONED_CHAIR_BACK.png"/><img src="reference/pixel-agents/assets/furniture/CUSHIONED_CHAIR/CUSHIONED_CHAIR_FRONT.png" width="16%" alt="CUSHIONED_CHAIR_FRONT.png" title="CUSHIONED_CHAIR_FRONT.png"/><img src="reference/pixel-agents/assets/furniture/CUSHIONED_CHAIR/CUSHIONED_CHAIR_SIDE.png" width="16%" alt="CUSHIONED_CHAIR_SIDE.png" title="CUSHIONED_CHAIR_SIDE.png"/>
</p>

#### `pixel-agents/assets/furniture/DESK`

<p>
<img src="reference/pixel-agents/assets/furniture/DESK/DESK_FRONT.png" width="16%" alt="DESK_FRONT.png" title="DESK_FRONT.png"/><img src="reference/pixel-agents/assets/furniture/DESK/DESK_SIDE.png" width="16%" alt="DESK_SIDE.png" title="DESK_SIDE.png"/>
</p>

#### `pixel-agents/assets/furniture/DOUBLE_BOOKSHELF`

<p>
<img src="reference/pixel-agents/assets/furniture/DOUBLE_BOOKSHELF/DOUBLE_BOOKSHELF.png" width="16%" alt="DOUBLE_BOOKSHELF.png" title="DOUBLE_BOOKSHELF.png"/>
</p>

#### `pixel-agents/assets/furniture/HANGING_PLANT`

<p>
<img src="reference/pixel-agents/assets/furniture/HANGING_PLANT/HANGING_PLANT.png" width="16%" alt="HANGING_PLANT.png" title="HANGING_PLANT.png"/>
</p>

#### `pixel-agents/assets/furniture/LARGE_PAINTING`

<p>
<img src="reference/pixel-agents/assets/furniture/LARGE_PAINTING/LARGE_PAINTING.png" width="16%" alt="LARGE_PAINTING.png" title="LARGE_PAINTING.png"/>
</p>

#### `pixel-agents/assets/furniture/LARGE_PLANT`

<p>
<img src="reference/pixel-agents/assets/furniture/LARGE_PLANT/LARGE_PLANT.png" width="16%" alt="LARGE_PLANT.png" title="LARGE_PLANT.png"/>
</p>

#### `pixel-agents/assets/furniture/PC`

<p>
<img src="reference/pixel-agents/assets/furniture/PC/PC_BACK.png" width="16%" alt="PC_BACK.png" title="PC_BACK.png"/><img src="reference/pixel-agents/assets/furniture/PC/PC_FRONT_OFF.png" width="16%" alt="PC_FRONT_OFF.png" title="PC_FRONT_OFF.png"/><img src="reference/pixel-agents/assets/furniture/PC/PC_FRONT_ON_1.png" width="16%" alt="PC_FRONT_ON_1.png" title="PC_FRONT_ON_1.png"/><img src="reference/pixel-agents/assets/furniture/PC/PC_FRONT_ON_2.png" width="16%" alt="PC_FRONT_ON_2.png" title="PC_FRONT_ON_2.png"/><img src="reference/pixel-agents/assets/furniture/PC/PC_FRONT_ON_3.png" width="16%" alt="PC_FRONT_ON_3.png" title="PC_FRONT_ON_3.png"/><img src="reference/pixel-agents/assets/furniture/PC/PC_SIDE.png" width="16%" alt="PC_SIDE.png" title="PC_SIDE.png"/>
</p>

#### `pixel-agents/assets/furniture/PLANT`

<p>
<img src="reference/pixel-agents/assets/furniture/PLANT/PLANT.png" width="16%" alt="PLANT.png" title="PLANT.png"/>
</p>

#### `pixel-agents/assets/furniture/PLANT_2`

<p>
<img src="reference/pixel-agents/assets/furniture/PLANT_2/PLANT_2.png" width="16%" alt="PLANT_2.png" title="PLANT_2.png"/>
</p>

#### `pixel-agents/assets/furniture/POT`

<p>
<img src="reference/pixel-agents/assets/furniture/POT/POT.png" width="16%" alt="POT.png" title="POT.png"/>
</p>

#### `pixel-agents/assets/furniture/SMALL_PAINTING`

<p>
<img src="reference/pixel-agents/assets/furniture/SMALL_PAINTING/SMALL_PAINTING.png" width="16%" alt="SMALL_PAINTING.png" title="SMALL_PAINTING.png"/>
</p>

#### `pixel-agents/assets/furniture/SMALL_PAINTING_2`

<p>
<img src="reference/pixel-agents/assets/furniture/SMALL_PAINTING_2/SMALL_PAINTING_2.png" width="16%" alt="SMALL_PAINTING_2.png" title="SMALL_PAINTING_2.png"/>
</p>

#### `pixel-agents/assets/furniture/SMALL_TABLE`

<p>
<img src="reference/pixel-agents/assets/furniture/SMALL_TABLE/SMALL_TABLE_FRONT.png" width="16%" alt="SMALL_TABLE_FRONT.png" title="SMALL_TABLE_FRONT.png"/><img src="reference/pixel-agents/assets/furniture/SMALL_TABLE/SMALL_TABLE_SIDE.png" width="16%" alt="SMALL_TABLE_SIDE.png" title="SMALL_TABLE_SIDE.png"/>
</p>

#### `pixel-agents/assets/furniture/SOFA`

<p>
<img src="reference/pixel-agents/assets/furniture/SOFA/SOFA_BACK.png" width="16%" alt="SOFA_BACK.png" title="SOFA_BACK.png"/><img src="reference/pixel-agents/assets/furniture/SOFA/SOFA_FRONT.png" width="16%" alt="SOFA_FRONT.png" title="SOFA_FRONT.png"/><img src="reference/pixel-agents/assets/furniture/SOFA/SOFA_SIDE.png" width="16%" alt="SOFA_SIDE.png" title="SOFA_SIDE.png"/>
</p>

#### `pixel-agents/assets/furniture/TABLE_FRONT`

<p>
<img src="reference/pixel-agents/assets/furniture/TABLE_FRONT/TABLE_FRONT.png" width="16%" alt="TABLE_FRONT.png" title="TABLE_FRONT.png"/>
</p>

#### `pixel-agents/assets/furniture/WHITEBOARD`

<p>
<img src="reference/pixel-agents/assets/furniture/WHITEBOARD/WHITEBOARD.png" width="16%" alt="WHITEBOARD.png" title="WHITEBOARD.png"/>
</p>

#### `pixel-agents/assets/furniture/WOODEN_BENCH`

<p>
<img src="reference/pixel-agents/assets/furniture/WOODEN_BENCH/WOODEN_BENCH.png" width="16%" alt="WOODEN_BENCH.png" title="WOODEN_BENCH.png"/>
</p>

#### `pixel-agents/assets/furniture/WOODEN_CHAIR`

<p>
<img src="reference/pixel-agents/assets/furniture/WOODEN_CHAIR/WOODEN_CHAIR_BACK.png" width="16%" alt="WOODEN_CHAIR_BACK.png" title="WOODEN_CHAIR_BACK.png"/><img src="reference/pixel-agents/assets/furniture/WOODEN_CHAIR/WOODEN_CHAIR_FRONT.png" width="16%" alt="WOODEN_CHAIR_FRONT.png" title="WOODEN_CHAIR_FRONT.png"/><img src="reference/pixel-agents/assets/furniture/WOODEN_CHAIR/WOODEN_CHAIR_SIDE.png" width="16%" alt="WOODEN_CHAIR_SIDE.png" title="WOODEN_CHAIR_SIDE.png"/>
</p>

#### `pixel-agents/assets/pets/claudio`

<p>
<img src="reference/pixel-agents/assets/pets/claudio/pet.png" width="16%" alt="pet.png" title="pet.png"/>
</p>

#### `pixel-agents/assets/pets/gitcat`

<p>
<img src="reference/pixel-agents/assets/pets/gitcat/pet.png" width="16%" alt="pet.png" title="pet.png"/>
</p>

#### `pixel-agents/assets/walls`

<p>
<img src="reference/pixel-agents/assets/walls/wall_0.png" width="16%" alt="wall_0.png" title="wall_0.png"/>
</p>

**`banner.png`**

<img width="100%" src="reference/pixel-agents/banner.png" alt="banner.png"/>

**`characters.png`**

<img width="100%" src="reference/pixel-agents/characters.png" alt="characters.png"/>

**`office.png`**

<img width="100%" src="reference/pixel-agents/office.png" alt="office.png"/>

**`Screenshot.jpg`**

<img width="100%" src="reference/pixel-agents/Screenshot.jpg" alt="Screenshot.jpg"/>

<p>
<img src="reference/pixel-agents/icon.png" width="16%" alt="icon.png" title="icon.png"/>
</p>

---

### 3d.city

[3d.city](https://github.com/lo-th/3d.city) — **1,744 ★** — `15` files in `reference/3d-city/`

#### `3d-city/img`

**`build_0.png`**

<img width="100%" src="reference/3d-city/img/build_0.png" alt="build_0.png"/>

**`build_1.png`**

<img width="100%" src="reference/3d-city/img/build_1.png" alt="build_1.png"/>

**`preview01.jpg`**

<img width="100%" src="reference/3d-city/img/preview01.jpg" alt="preview01.jpg"/>

**`preview02.jpg`**

<img width="100%" src="reference/3d-city/img/preview02.jpg" alt="preview02.jpg"/>

**`preview03.jpg`**

<img width="100%" src="reference/3d-city/img/preview03.jpg" alt="preview03.jpg"/>

**`tuto.png`**

<img width="100%" src="reference/3d-city/img/tuto.png" alt="tuto.png"/>

<p>
<img src="reference/3d-city/img/stripe_l.png" width="16%" alt="stripe_l.png" title="stripe_l.png"/><img src="reference/3d-city/img/stripe_r.png" width="16%" alt="stripe_r.png" title="stripe_r.png"/>
</p>

#### `3d-city/textures`

**`building.png`**

<img width="100%" src="reference/3d-city/textures/building.png" alt="building.png"/>

**`cars.png`**

<img width="100%" src="reference/3d-city/textures/cars.png" alt="cars.png"/>

**`ground1k.png`**

<img width="100%" src="reference/3d-city/textures/ground1k.png" alt="ground1k.png"/>

**`road.png`**

<img width="100%" src="reference/3d-city/textures/road.png" alt="road.png"/>

**`tiles.png`**

<img width="100%" src="reference/3d-city/textures/tiles.png" alt="tiles.png"/>

**`title.png`**

<img width="100%" src="reference/3d-city/textures/title.png" alt="title.png"/>

**`town.png`**

<img width="100%" src="reference/3d-city/textures/town.png" alt="town.png"/>

---

### JSCity

[JSCity](https://github.com/aserg-ufmg/JSCity) — **1,400 ★** — `80` files in `reference/jscity/`

#### `jscity/cities`

**`ace.png`**

<img width="100%" src="reference/jscity/cities/ace.png" alt="ace.png"/>

**`algorithmsjs.png`**

<img width="100%" src="reference/jscity/cities/algorithmsjs.png" alt="algorithmsjs.png"/>

**`algoritmsjs.png`**

<img width="100%" src="reference/jscity/cities/algoritmsjs.png" alt="algoritmsjs.png"/>

**`angular.png`**

<img width="100%" src="reference/jscity/cities/angular.png" alt="angular.png"/>

**`angularjs.png`**

<img width="100%" src="reference/jscity/cities/angularjs.png" alt="angularjs.png"/>

**`backbone.png`**

<img width="100%" src="reference/jscity/cities/backbone.png" alt="backbone.png"/>

**`bootstrap.png`**

<img width="100%" src="reference/jscity/cities/bootstrap.png" alt="bootstrap.png"/>

**`bower.png`**

<img width="100%" src="reference/jscity/cities/bower.png" alt="bower.png"/>

**`cappuccino.png`**

<img width="100%" src="reference/jscity/cities/cappuccino.png" alt="cappuccino.png"/>

**`chart.png`**

<img width="100%" src="reference/jscity/cities/chart.png" alt="chart.png"/>

**`chartjs.png`**

<img width="100%" src="reference/jscity/cities/chartjs.png" alt="chartjs.png"/>

**`clumsy-bird.png`**

<img width="100%" src="reference/jscity/cities/clumsy-bird.png" alt="clumsy-bird.png"/>

**`clumsybird.png`**

<img width="100%" src="reference/jscity/cities/clumsybird.png" alt="clumsybird.png"/>

**`crafty.png`**

<img width="100%" src="reference/jscity/cities/crafty.png" alt="crafty.png"/>

**`d3js.png`**

<img width="100%" src="reference/jscity/cities/d3js.png" alt="d3js.png"/>

**`Deck.png`**

<img width="100%" src="reference/jscity/cities/Deck.png" alt="Deck.png"/>

**`deckjs.png`**

<img width="100%" src="reference/jscity/cities/deckjs.png" alt="deckjs.png"/>

**`dexter.png`**

<img width="100%" src="reference/jscity/cities/dexter.png" alt="dexter.png"/>

**`dojo.png`**

<img width="100%" src="reference/jscity/cities/dojo.png" alt="dojo.png"/>

**`dust.png`**

<img width="100%" src="reference/jscity/cities/dust.png" alt="dust.png"/>

**`easelJs.png`**

<img width="100%" src="reference/jscity/cities/easelJs.png" alt="easelJs.png"/>

**`ember.png`**

<img width="100%" src="reference/jscity/cities/ember.png" alt="ember.png"/>

**`express.png`**

<img width="100%" src="reference/jscity/cities/express.png" alt="express.png"/>

**`florajs.png`**

<img width="100%" src="reference/jscity/cities/florajs.png" alt="florajs.png"/>

**`ghost.png`**

<img width="100%" src="reference/jscity/cities/ghost.png" alt="ghost.png"/>

**`grunt.png`**

<img width="100%" src="reference/jscity/cities/grunt.png" alt="grunt.png"/>

**`gulp.png`**

<img width="100%" src="reference/jscity/cities/gulp.png" alt="gulp.png"/>

**`impress.png`**

<img width="100%" src="reference/jscity/cities/impress.png" alt="impress.png"/>

**`impressjs.png`**

<img width="100%" src="reference/jscity/cities/impressjs.png" alt="impressjs.png"/>

**`intern.png`**

<img width="100%" src="reference/jscity/cities/intern.png" alt="intern.png"/>

**`ionic.png`**

<img width="100%" src="reference/jscity/cities/ionic.png" alt="ionic.png"/>

**`isome.png`**

<img width="100%" src="reference/jscity/cities/isome.png" alt="isome.png"/>

**`isomer.png`**

<img width="100%" src="reference/jscity/cities/isomer.png" alt="isomer.png"/>

**`istanbul.png`**

<img width="100%" src="reference/jscity/cities/istanbul.png" alt="istanbul.png"/>

**`jade.png`**

<img width="100%" src="reference/jscity/cities/jade.png" alt="jade.png"/>

**`jasmine (2).png`**

<img width="100%" src="reference/jscity/cities/jasmine (2).png" alt="jasmine (2).png"/>

**`jasmine.png`**

<img width="100%" src="reference/jscity/cities/jasmine.png" alt="jasmine.png"/>

**`jasmini.png`**

<img width="100%" src="reference/jscity/cities/jasmini.png" alt="jasmini.png"/>

**`jquery-file-upload.png`**

<img width="100%" src="reference/jscity/cities/jquery-file-upload.png" alt="jquery-file-upload.png"/>

**`jquery.png`**

<img width="100%" src="reference/jscity/cities/jquery.png" alt="jquery.png"/>

**`jqueryfileupload.png`**

<img width="100%" src="reference/jscity/cities/jqueryfileupload.png" alt="jqueryfileupload.png"/>

**`js-git.png`**

<img width="100%" src="reference/jscity/cities/js-git.png" alt="js-git.png"/>

**`karma.png`**

<img width="100%" src="reference/jscity/cities/karma.png" alt="karma.png"/>

**`knockout.png`**

<img width="100%" src="reference/jscity/cities/knockout.png" alt="knockout.png"/>

**`leaflet.png`**

<img width="100%" src="reference/jscity/cities/leaflet.png" alt="leaflet.png"/>

**`less.png`**

<img width="100%" src="reference/jscity/cities/less.png" alt="less.png"/>

**`meteor.png`**

<img width="100%" src="reference/jscity/cities/meteor.png" alt="meteor.png"/>

**`mocha.png`**

<img width="100%" src="reference/jscity/cities/mocha.png" alt="mocha.png"/>

**`modernizr.png`**

<img width="100%" src="reference/jscity/cities/modernizr.png" alt="modernizr.png"/>

**`mootools.png`**

<img width="100%" src="reference/jscity/cities/mootools.png" alt="mootools.png"/>

**`move.png`**

<img width="100%" src="reference/jscity/cities/move.png" alt="move.png"/>

**`mustache.png`**

<img width="100%" src="reference/jscity/cities/mustache.png" alt="mustache.png"/>

**`paper.png`**

<img width="100%" src="reference/jscity/cities/paper.png" alt="paper.png"/>

**`paperjs.png`**

<img width="100%" src="reference/jscity/cities/paperjs.png" alt="paperjs.png"/>

**`parallax.png`**

<img width="100%" src="reference/jscity/cities/parallax.png" alt="parallax.png"/>

**`pdfjs.png`**

<img width="100%" src="reference/jscity/cities/pdfjs.png" alt="pdfjs.png"/>

**`phase.png`**

<img width="100%" src="reference/jscity/cities/phase.png" alt="phase.png"/>

**`pixi.png`**

<img width="100%" src="reference/jscity/cities/pixi.png" alt="pixi.png"/>

**`pug.png`**

<img width="100%" src="reference/jscity/cities/pug.png" alt="pug.png"/>

**`quintus.png`**

<img width="100%" src="reference/jscity/cities/quintus.png" alt="quintus.png"/>

**`react.png`**

<img width="100%" src="reference/jscity/cities/react.png" alt="react.png"/>

**`respond.png`**

<img width="100%" src="reference/jscity/cities/respond.png" alt="respond.png"/>

**`reveal.png`**

<img width="100%" src="reference/jscity/cities/reveal.png" alt="reveal.png"/>

**`riot.png`**

<img width="100%" src="reference/jscity/cities/riot.png" alt="riot.png"/>

**`rot.png`**

<img width="100%" src="reference/jscity/cities/rot.png" alt="rot.png"/>

**`select2.png`**

<img width="100%" src="reference/jscity/cities/select2.png" alt="select2.png"/>

**`semantic-ui.png`**

<img width="100%" src="reference/jscity/cities/semantic-ui.png" alt="semantic-ui.png"/>

**`semanticui.png`**

<img width="100%" src="reference/jscity/cities/semanticui.png" alt="semanticui.png"/>

**`slick.png`**

<img width="100%" src="reference/jscity/cities/slick.png" alt="slick.png"/>

**`snap.png`**

<img width="100%" src="reference/jscity/cities/snap.png" alt="snap.png"/>

**`socket.io.png`**

<img width="100%" src="reference/jscity/cities/socket.io.png" alt="socket.io.png"/>

**`soket.io.png`**

<img width="100%" src="reference/jscity/cities/soket.io.png" alt="soket.io.png"/>

**`textillate.png`**

<img width="100%" src="reference/jscity/cities/textillate.png" alt="textillate.png"/>

**`threejs.png`**

<img width="100%" src="reference/jscity/cities/threejs.png" alt="threejs.png"/>

**`tween.png`**

<img width="100%" src="reference/jscity/cities/tween.png" alt="tween.png"/>

**`underscore.png`**

<img width="100%" src="reference/jscity/cities/underscore.png" alt="underscore.png"/>

**`velocity.png`**

<img width="100%" src="reference/jscity/cities/velocity.png" alt="velocity.png"/>

**`zepto.png`**

<img width="100%" src="reference/jscity/cities/zepto.png" alt="zepto.png"/>

<p>
<img src="reference/jscity/favicon.png" width="16%" alt="favicon.png" title="favicon.png"/><img src="reference/jscity/rect.png" width="16%" alt="rect.png" title="rect.png"/>
</p>

---

### agent-office

[agent-office](https://github.com/harishkotra/agent-office) — **265 ★** — `7` files in `reference/agent-office/`

**`characters.png`**

<img width="100%" src="reference/agent-office/characters.png" alt="characters.png"/>

<p>
<img src="reference/agent-office/char_0.png" width="16%" alt="char_0.png" title="char_0.png"/><img src="reference/agent-office/char_1.png" width="16%" alt="char_1.png" title="char_1.png"/><img src="reference/agent-office/char_2.png" width="16%" alt="char_2.png" title="char_2.png"/><img src="reference/agent-office/char_3.png" width="16%" alt="char_3.png" title="char_3.png"/><img src="reference/agent-office/char_4.png" width="16%" alt="char_4.png" title="char_4.png"/><img src="reference/agent-office/char_5.png" width="16%" alt="char_5.png" title="char_5.png"/>
</p>

---

### city-tour

[city-tour](https://github.com/jstrait/city-tour) — **88 ★** — `2` files in `reference/city-tour/`

**`city_tour.gif`**

<img width="100%" src="reference/city-tour/city_tour.gif" alt="city_tour.gif"/>

<p>
<img src="reference/city-tour/grid.png" width="16%" alt="grid.png" title="grid.png"/>
</p>

---

### agent-town

[agent-town](https://github.com/rafapetter/agent-town) — **5 ★** — `11` files in `reference/agent-town/`

**`dashboard-agents.png`**

<img width="100%" src="reference/agent-town/dashboard-agents.png" alt="dashboard-agents.png"/>

**`dashboard-analytics.png`**

<img width="100%" src="reference/agent-town/dashboard-analytics.png" alt="dashboard-analytics.png"/>

**`dashboard-kanban.png`**

<img width="100%" src="reference/agent-town/dashboard-kanban.png" alt="dashboard-kanban.png"/>

**`dashboard-timeline.png`**

<img width="100%" src="reference/agent-town/dashboard-timeline.png" alt="dashboard-timeline.png"/>

**`playground-agents.png`**

<img width="100%" src="reference/agent-town/playground-agents.png" alt="playground-agents.png"/>

**`playground-farm.png`**

<img width="100%" src="reference/agent-town/playground-farm.png" alt="playground-farm.png"/>

**`playground-office.png`**

<img width="100%" src="reference/agent-town/playground-office.png" alt="playground-office.png"/>

**`playground-pirate-ship.png`**

<img width="100%" src="reference/agent-town/playground-pirate-ship.png" alt="playground-pirate-ship.png"/>

**`playground-rocket.png`**

<img width="100%" src="reference/agent-town/playground-rocket.png" alt="playground-rocket.png"/>

**`playground-space-station.png`**

<img width="100%" src="reference/agent-town/playground-space-station.png" alt="playground-space-station.png"/>

**`playground-town.png`**

<img width="100%" src="reference/agent-town/playground-town.png" alt="playground-town.png"/>

---

### CodeCity

[CodeCity](https://wettel.github.io/codecity.html) — **— ★** — `12` files in `reference/code-city/`

**`codecity-ated-ict-2008.png`**

<img width="100%" src="reference/code-city/codecity-ated-ict-2008.png" alt="codecity-ated-ict-2008.png"/>

**`codecity-screenshot.png`**

<img width="100%" src="reference/code-city/codecity-screenshot.png" alt="codecity-screenshot.png"/>

**`gource-git.jpg`**

<img width="100%" src="reference/code-city/gource-git.jpg" alt="gource-git.jpg"/>

**`gource-linux.jpg`**

<img width="100%" src="reference/code-city/gource-linux.jpg" alt="gource-linux.jpg"/>

**`gource-papervision.jpg`**

<img width="100%" src="reference/code-city/gource-papervision.jpg" alt="gource-papervision.jpg"/>

#### `code-city/wof`

**`argouml.png`**

<img width="100%" src="reference/code-city/wof/argouml.png" alt="argouml.png"/>

**`codecity.png`**

<img width="100%" src="reference/code-city/wof/codecity.png" alt="codecity.png"/>

**`jdk.png`**

<img width="100%" src="reference/code-city/wof/jdk.png" alt="jdk.png"/>

**`jhotdraw7.png`**

<img width="100%" src="reference/code-city/wof/jhotdraw7.png" alt="jhotdraw7.png"/>

**`jmol.png`**

<img width="100%" src="reference/code-city/wof/jmol.png" alt="jmol.png"/>

**`moose-suite.png`**

<img width="100%" src="reference/code-city/wof/moose-suite.png" alt="moose-suite.png"/>

**`vuze.png`**

<img width="100%" src="reference/code-city/wof/vuze.png" alt="vuze.png"/>

---

## `> data_sources`

**Transcripts primary, hooks optional.** `~/.claude/projects/<slug>/<uuid>.jsonl`, one
JSON object per line, appended live. Confirmed fields include `isSidechain` (this is
how subagents get bodies), `uuid` / `parentUuid` (causality, not just order),
`timestamp`, `durationMs`, `cwd`, `gitBranch` and full `tool_use` blocks.

```bash
you@github:~$ ls ~/.claude/projects/

  SESSIONS:       1,553 .jsonl files
  SIZE:           2.5 GB
  LARGEST:        17,256 lines in one session
  SUBAGENTS:      flagged inline via isSidechain
```

> **Hooks give you the future. Transcripts give you the past.** `pixel-agents` uses
> hooks as primary, which proves the per-call latency is tolerable - but hooks cannot
> retroactively recover a single one of those 1,553 sessions. The chronicle is the
> distinctive half of this project, so transcripts lead and hooks are a live-fidelity
> upgrade. Copy the `pixel-agents` pattern: one event model, one provider interface,
> renderer never knows which source fed it.

---

## `> what_this_changes`

Four things worth stealing outright:

| From | Steal |
|:--|:--|
| `token-dashboard` | The whole pipeline shape - Python stdlib + SQLite + vanilla JS, no build step. Already the house pattern, and the 20-60 s scan figure makes M0 an evening |
| `JSCity` | The metric mapping. Do not re-derive what height and footprint should mean |
| `AI Town` | "Historical objects" - client-side interpolation between sparse, lumpy state updates. Exactly the problem a tool-call-driven city has |
| `pixel-agents` | The dual-source provider interface, the activity-driven character animation, and the `furniture/*/manifest.json` sprite format |

And one thing to be honest about: **the overlap with `pixel-agents` on the live half is
substantial.** Reading or forking it beats rebuilding the citizen layer. The novel
work here is the terrain and the chronicle.

---

## `> tree`

```bash
Agent City/
├── README.md                 # this file
├── IDEA.md                   # the full design doc
└── reference/                # competitor assets, mirrored for study
    ├── README.md             # the three design patterns, side by side
    ├── ATTRIBUTION.md        # licences + what was deliberately NOT mirrored
    ├── generative-agents/    # 22,087 ★ Smallville map + characters + tiles
    ├── gource/               # 13,138 ★ beam/file/user sprites
    ├── ai-town/              # 10,473 ★ tilesets, spritesheets, UI
    ├── pixel-agents/         #  9,243 ★ office furniture + character sheets
    ├── 3d-city/              #  1,744 ★ previews + building textures
    ├── jscity/               #  1,400 ★ 60 city stills (Angular, jQuery, …)
    ├── agent-office/         #    265 ★ character sprites
    ├── city-tour/            #     88 ★ city_tour.gif
    ├── agent-town/           #      5 ★ 11 screenshots, 7 themed playgrounds
    └── code-city/            # academic original + Wall of Fame stills
```

---

## `> build_order`

| Milestone | What | Effort |
|:--|:--|:--|
| **M0** | Corpus survey - parse all 1,553 transcripts into `city.db` | One evening |
| **M1** | Static skyline - one district from a filesystem walk, no motion | |
| **M2** | Chronicle - replay one recorded session over M1, with a scrub bar | |
| **M3** | Live City - tail the active session file | |
| **M4** | Whole-corpus timelapse + video export | The shareable artifact |
| **M5** | Packaging - pywebview shell, tray icon, autostart | |

M0 through M2 is the honest minimum for something worth showing.

---

## `> stats --live`

| METRIC | COUNT | NOTES |
|:------:|:-----:|:-----:|
| **Sessions on disk** | `1,553` | `~/.claude/projects/**/*.jsonl` |
| **Corpus size** | `2.5 GB` | Grows every session |
| **Largest session** | `17,256` | Lines in one `.jsonl` |
| **Prior-art projects surveyed** | `15` | Across three camps, tables sorted by stars |
| **Reference assets mirrored** | `350` images | All embedded in this README. 40 MB under `reference/`, licences in `ATTRIBUTION.md` |
| **Lines of Agent City code** | `0` | Idea stage |

---

## `> related_projects`

| Repo | What |
|:-----|:-----|
| [Ringmast4r/argus](https://github.com/Ringmast4r/argus) | Globe visualisation - the other big render project |
| [Ringmast4r/Gods-Eye-Index](https://github.com/Ringmast4r/Gods-Eye-Index) | DB-generated README, same "db is truth" pattern |

<div align="center">

**Maintained by** [@Ringmast4r](https://github.com/Ringmast4r)

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:A21CAF,100:000000&height=120&section=footer&text=Every%20citizen%20is%20a%20real%20tool%20call&fontSize=18&fontColor=ffffff&fontAlignY=65"/>

</div>
