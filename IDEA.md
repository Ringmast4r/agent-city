# Agent City

An isometric city that is built, populated and run by my own Claude Code sessions.
Every project is a district, every file is a building, every agent is a little person
walking around doing the work. Live while a session runs, and replayable across the
1,553 sessions already sitting on disk.

Status: idea only, nothing built yet. Written 2026-09-11.

---

## 1. What this actually is

Two separate traditions that nobody has properly welded together yet.

**Code-as-city** (the buildings)
- CodeCity, Richard Wettel 2008 - packages are districts, classes are buildings,
  methods are floors, attributes are the footprint. The original.
- Gource - repo history as an animated tree, committers as avatars pushing files
  around. Everyone has seen the timelapse videos.
- Evo Streets and the rest of the "software as a city" family - street layouts
  instead of blocks.

**Agent-as-citizen** (the people)
- Generative Agents / Smallville, Park et al. 2023 - LLM agents living in a pixel
  town. The paper that started the whole look.
- AI Town (a16z-infra) - the Stardew-Valley-style open source version people fork.
- The current crop of "watch my agent swarm work" posts - little sprites labelled
  with tool names, mostly hand-faked for the video.

The core principle: **the city is not a simulation, it is a read-out.** Every person
on screen is an actual tool call that actually happened.

**Correction after the 2026-09-11 survey** (full results in [README.md](README.md)):
the original draft of this doc claimed nobody was driving the citizen layer with real
agent telemetry. That is false. **pixel-agents** (9.2k stars) already does exactly
that for Claude Code, via hooks with a JSONL fallback. What is still genuinely unclaimed
is the *join*: real terrain generated from the actual file tree, walked by real
citizens, over a real time axis, with a 1,553-session back catalogue to replay. The
people camp uses fictional maps; the buildings camp has no people and no clock.

---

## 2. Why this is easy here specifically

The hard part is already done, and it was done by accident: a long, dense, honest
event log.

| Asset | Amount |
|---|---|
| Session transcripts (`~/.claude/projects/**/*.jsonl`) | 1,553 files, 2.5 GB |
| Biggest single session | 17,256 lines |
| Distinct project roots | 2 cwd slugs, but dozens of real project dirs inside |
| Library districts already numbered | `D:\00` through `D:\27`, plus E: and F: |

The `D:` drive numbering (00 Database Library, 01 GITHUB Library, ... 27 Chrome
Extensions Library) is *already a city plan*. Those are the districts. The layout
does not need inventing - it has been maintained for months without noticing.

---

## 3. Data sources, in order of preference

### 3.1 Transcript tailing (primary - use this)

`C:\Users\Squir\.claude\projects\<cwd-slug>\<session-uuid>.jsonl`, one JSON object
per line, appended live as the session runs. Fields confirmed by inspection:

```
type            user | assistant | mode | permission-mode | summary | ...
uuid, parentUuid    the conversation DAG - gives causality, not just order
isSidechain     true = this is a SUBAGENT turn. This is how agents get bodies.
timestamp       ISO8601 UTC - the clock the whole city runs on
message         role + content[], incl. tool_use blocks (name + input) and results
toolUseResult   the outcome, including errors
durationMs      how long the call took - walking speed, how long a light stays on
cwd, gitBranch  which district, which era
sessionId       which mayor
version         Claude Code version - buildings can age by era
effort, perTurnEffort   thinking effort - citizen intensity
requestId, apiBlockIndex
```

Everything needed is here. **No hooks required for v1**, and no latency added to
real work. Tail the newest-mtime file in the projects dir, or watch them all.

### 3.2 Hooks (secondary, but less optional than first thought)

**Revised 2026-09-11.** pixel-agents uses hooks as its *primary* source and JSONL only
as a fallback, which is real-world evidence that the per-call latency is tolerable.
The correct framing is not either/or:

- **Hooks give you the future** - low latency, plus permission and notification events
  the transcripts never record at all.
- **Transcripts give you the past** - all 1,553 sessions, retroactively. Hooks cannot
  recover a single one of those, ever.

The chronicle is the distinctive half of this project, so transcripts stay primary and
hooks become an optional live-fidelity upgrade. Copy the pixel-agents pattern:
normalise both sources into one event model behind one typed provider interface, so
the renderer never knows which one it is being fed.


`PreToolUse / PostToolUse / UserPromptSubmit / SessionStart / Stop / SubagentStop /
Notification / PreCompact` in `~/.claude/settings.json`.

Only worth adding for permission prompts and denials, notification and idle events,
and precise sub-second start/stop edges.

**Trap:** the hook command runs on *every single tool call*. `powershell -c` costs
roughly 200 ms of process startup and `python -c` roughly 50 ms, which would be felt
all day, on every call, forever. If this happens at all the hook must be a Git Bash
`cat >> events.ndjson` or a tiny compiled appender. Measure before committing to it.

### 3.3 Filesystem and git (the terrain)

Walk each project root once per district to get the buildings that exist: path, size,
LOC, extension, mtime. `git log` gives commit trucks and building age. This is the
static map the citizens then walk around on.

---

## 4. The mapping (the fun part)

**Terrain**
- District = a project root or library folder. `D:\03 Website Library` is one
  neighbourhood, `D:\24 Geospatial Library` another. Numbered districts sit in
  numbered order around a central square, so the city is navigable by muscle memory.
- Block = a subdirectory. Road = the directory tree.
- Building = a file. Footprint = file size, height = lines of code, window count =
  functions or headings. Grey concrete = untouched, lit windows = touched this session.
- Patina = git last-modified. Dead code goes mossy.
- Offshore island = GitHub. Harbour = the open internet (WebFetch, WebSearch, APIs).
- Power station district on the edge of town = the R630 and its LXC containers, one
  cooling tower per CT, lit when that container is up.

**Citizens**
- Main session = the Mayor, one per session, walks out of City Hall when I type.
- Subagent (`isSidechain: true`) = a worker who leaves City Hall, walks to a district,
  does the job, walks back and files a report. Parallel agents are literally a crowd.
- Model = the uniform. Opus, Sonnet and Haiku get distinct silhouettes and colours.
- Effort level = pace. `xhigh` citizens move deliberately, with a thought bubble.

**Actions - tool calls become verbs**

| Tool | What the city shows |
|---|---|
| Read | Citizen enters the building, a window lights up |
| Edit / Write | Scaffolding and a crane; the building grows on save |
| Bash / PowerShell | A truck drives the road |
| Grep / Glob | A searchlight sweeps the district, hits flash |
| WebFetch / WebSearch | Boat or plane leaves the harbour, returns loaded |
| Agent (spawn) | A bus leaves City Hall carrying workers |
| Error / non-zero exit | Smoke from that roof; repeated errors become a fire |
| Git commit | Convoy leaves the district toward the offshore island |
| Compaction | Fog rolls over the oldest streets and they grey out |
| Token spend | Street-light brightness, and a grid-load meter |
| Session end | Lights go out district by district, streetlights stay on |

**Hard rule: every animation encodes data.** No decorative glow, no idle sparkle, no
motion that does not mean a real event happened. If it moves, something happened.

---

## 5. Two modes

**Live City.** Tail the active session's `.jsonl`. The city moves as I work. This is
the second-monitor toy, and the thing that makes people ask what they are looking at.

**Chronicle.** Replay any past session, or the whole 1,553-session corpus, as a
timelapse. Scrub bar, speed control, jump to a session. This is the real artifact:
*here is every hour of work I have done this year, rendered as a city being built.*
A one-minute export of that is a strong conference or Substack piece, and there is
already a Presentations folder and a Substack library to put it in.

---

## 6. Stack

Chosen to reuse what is already known to work on this machine.

- **Three.js with an orthographic camera** for the isometric look. Low-poly boxes and
  flat colour first - zero textures, zero asset pipeline. Already proven on the Clippy
  extension, so the renderer is known to behave here.
- **SQLite `city.db` as the source of truth.** The parser reads 2.5 GB of JSONL once
  and writes a normalised event table. The renderer only ever reads the db, never the
  raw transcripts. Same house pattern as every other project: db is truth, the view is
  generated from it.
- **Delivery: a pywebview desktop app.** Single window, loads local HTML, pushes events
  into the page with `evaluate_js`. No local dev server - that rule stands.
  - *Trap:* pywebview walks every public attribute of `js_api` and recurses. Underscore
    anything not meant to be exposed.
- **Alternative delivery** if it should be shareable: generate a static site from
  `city.db` and put it on its own CT behind a tunnel, replay-only. Live mode stays
  desktop-only because it needs the local file tail.
- **Windows tray icon** for the live watcher so it can sit running all day. The AUMID
  plus Start Menu shortcut trick for real toasts is already solved.

Machine traps to respect: stdlib `json` only (orjson silently breaks dict key lookups
here), no PIL text rendering under Python 3.14, and never put a Windows path inside a
Python string inside a Bash heredoc.

---

## 7. Build order

- **M0 - Corpus survey.** Parse all 1,553 transcripts into `city.db`. Answer: total
  tool calls, which tools dominate, how many subagent turns, how many distinct file
  paths touched, full date range. This is an interesting stat sheet on its own and it
  de-risks everything downstream. Worth doing even if the rest never happens.
- **M1 - Static skyline.** One district, rendered from a filesystem walk, no motion.
  Prove the isometric layout reads well and that buildings are distinguishable.
- **M2 - Chronicle.** Replay one recorded session over M1. Citizens walk, windows light,
  cranes go up. Scrub bar.
- **M3 - Live City.** Tail the active session file. Same renderer, new source.
- **M4 - Whole-corpus timelapse plus video export.** The shareable artifact.
- **M5 - Packaging.** pywebview shell, tray icon, autostart.

M0 through M2 is the honest minimum for something worth showing. M0 is one evening.

---

## 8. Open questions to settle before building

1. **Building identity across a 2.5 GB corpus.** Thousands of distinct file paths across
   dozens of project roots - does the whole city render at once, or one district at a
   time under a zoomed-out world map? Leaning toward a world map that zooms into a
   district.
2. **Time compression.** Real sessions have long thinking gaps and 40-second bash runs.
   Live mode wants a wall clock; chronicle mode needs an event-density clock or it is
   90 percent empty road.
3. **Path privacy.** The transcripts carry client work, case books and real file paths.
   Anything exported publicly needs a scrub layer - district names hashed or aliased -
   and it belongs at the db layer, not the render layer.
4. **Sprite art.** Flat geometric citizens that can be generated, or actual pixel
   sprites? Kenney's isometric city kit is CC0 and would cut M1 to almost nothing.
5. **Personal, or a hub tile?** It could live behind the hub gate with the other tools,
   but a chronicle of my own work is arguably a portfolio piece for ringmast4r.com.

---

## 9. When this becomes a repo

Per the project repo memorandum: one private repo, README opens with the full banner
in its own unique colour, commit and push every session. Colour not yet claimed - pick
one no existing project banner is using.

Layout, matching the house standard:

```
Agent City/
  data/     city.db (source of truth) + raw/ sample transcripts for tests
  scripts/  parse_transcripts.py, build_city.py, watch_live.py
  public/   index.html, city.js, data.js (generated from the db)
  app/      pywebview shell and tray icon
  docs/     IDEA.md (this file), MAPPING.md (section 4, frozen once agreed)
  tests/
  README.md
```
