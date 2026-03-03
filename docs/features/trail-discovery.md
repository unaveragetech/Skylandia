# 🧭 Trail Discovery System

> *Autonomous exploration that hunts the past while you sleep.*

The Trail Discovery System is Skylandia’s flagship exploration capability — a three-module pipeline that turns the chaos of an infinite Minecraft world into a navigable map of player history and forgotten terrain.

Most anarchy tools show you what’s around you. This system **chases what was there before you**.

---

## The Three Modules

### Trails — The Analyst

Trails is one of the most technically sophisticated chunk classification engines in any client addon. Every chunk that loads is passed through a configurable set of forensic detectors and assigned one of five distinct types:

| Chunk Type | Meaning |
|-----------|--------|
| `NEW` | Generated after the world border was last active — no player has been here |
| `OLD` | Generated in a previous version, likely untouched for years |
| `BEING_UPDATED` | Currently migrating from a pre-1.17 generation pattern |
| `OLD_GENERATION` | Legacy generation signature confirmed by block palette analysis |
| `TICK_EXPLOIT` | Flagged via block update timing anomalies |

Each type is rendered in a distinct configurable color and tracked separately.

**Detection methods (independently toggleable):**

| Method | How it works |
|--------|-------------|
| **Palette Exploit Detection** | Analyzes the ordering of chunk section block palettes. The order in which blocks appear in a new 1.18+ chunk’s palette is deterministic — if it doesn’t match that signature, the chunk is old or touched. |
| **Legacy Chunk Update Detection** | Marks chunks migrating from pre-1.17 as `BEING_UPDATED` — these are live conversion events you can watch happen. |
| **Overworld Old Chunk Detector** | Checks for blocks above Y=0 that only exist in pre-1.17 worlds. If they’re there, the chunk predates the Caves & Cliffs update. |
| **Nether Old Chunk Detector** | Checks for missing Nether 1.16 blocks. Pre-Nether-Update chunks lack warped/crimson forest terrain. |
| **End Old Chunk Detector** | Detects chunks biome-typed as `the_end` only — a signature of pre-1.13 End generation. |
| **Real-Time Detection** | Processes chunk data packets as they arrive for immediate feedback. |
| **Liquid Exploit Detection** | Infers chunk age from flowing liquid patterns in newly loaded terrain. |
| **Block Update Exploit Detection** | Tracks block update packets to flag recently touched areas. |

**Additional settings groups:**
- **Detection Sensitivity** — tune false-positive tolerance per method
- **Saved / Cached Chunk Data** — persist classifications across sessions
- **Per-Chunk-Type Settings** — independent color, render, and notification settings per type
- **Notifications** — Discord webhook integration per chunk type
- **Performance** — throttle processing to cap CPU impact

XaeroPlus modules (`PaletteNewChunks`, `OldChunks`) are queried for cross-reference confirmation when available.

---

### TrailFollower — The Strategist

TrailFollower reads the Trails layer in real time and navigates toward it. When player-touched or historically loaded chunks appear, it weighs them against your configured rules and steers you on an optimal bearing — automatically.

When the trail runs cold, it executes a configurable fallback: spiral outward, hold position, return to last known point, or shut down and log your position.

**Key settings:**
- `visitedChunkInfluence` — ignore, avoid, or prefer already-covered chunks
- `trailEndBehavior` — what to do when no new trail signal is found
- `maxTrailDeviation` — hard angle limit before abandoning a bearing
- `startDirectionWeighting` — bias toward your original heading for organic paths
- `autoDisconnect` — safety logout if load rate spikes unexpectedly

---

### AFKVanillaFly — The Pilot

Maintains locked-altitude high-speed elytra flight indefinitely without input. Monitors velocity, fires fireworks at the exact moment to avoid speed drop, and can hand control back to TrailFollower after long legs.

---

## CoordPoppy — The Map Layer

Once the trail pipeline has run, **CoordPoppy** renders it all. CoordPoppy is Skylandia’s advanced minimap system — far beyond what any standard minimap provides:

- **Randar exploit integration** — correlates RNG seed output with entity positions to locate players remotely
- **Remote Entity Detector** — flags entities that shouldn’t be present based on activity patterns
- **Player Activity Tracker** — logs player presence patterns over time
- **Trails integration** — overlays NEW/OLD/BEING_UPDATED chunk classifications directly on the map
- **TrailFollower integration** — shows the follower’s current bearing and target on the map
- **LocationSpoofer** — masks your real coordinates from server-side queries
- **ChunkAnalyzer** — processes chunk structure for advanced pattern matching
- **SwarmIntegration** — coordinate with other Skylandia instances via a shared data channel
- **Discord webhook support** — auto-alert on significant discoveries

CoordPoppy is its own subsystem with six internal components, making it one of the most capable reconnaissance surfaces in any Minecraft client mod.

---

## Other Exploration & Hunting Modules

The Trail Discovery System and CoordPoppy are the headliners, but the Exploration category contains many more modules:

### BetterStashFinder
Scans every incoming chunk’s block entity data for storage containers (chests, barrels, shulker boxes). Also runs asynchronous structure detection: **villages** are flagged by iron golems and villager presence, **trial chambers** by trial spawner entities and Breezes, **dungeons** by spawner type signatures. Player detection fires a Discord webhook with a 5-minute re-alert interval. Auto-screenshots discoverie. Xaero waypoint creation on hit. Runs with a dedicated thread pool so chunk scanning never blocks the main thread.

### SmartActionBot
Natural language command executor. Accepts commands like `"walk to 100 64 200"` via an internal queue, parses them, and executes through Baritone navigation + input simulation. Simultaneously handles inventory management, food/health monitoring, and basic combat while traveling. Built with an LLM integration stub — commands can be fed from chat, from an external socket, or from OllamaBotModule. Visited-position tracking prevents loops.

### BaseFinder
Detects base-like structures from block density and entity patterns in loaded chunks. Scores candidate positions and logs high-confidence hits with coordinates and confidence rating.

### CaveDisturbanceDetector
Flags terrain that shows signs of player interaction: placed torches, non-natural block transitions, cleared cave sections. Useful for following fresh trails downward.

### StashBotModule
Automated stash logging pipeline. Receives hits from BetterStashFinder, writes them to a local log with timestamp and dimension, creates Xaero waypoints, and fires configurable Discord alerts.

### TerrainAnalyzer
Profiles terrain across the loaded area for travel efficiency, choke-point mapping, and PvP positioning. Outputs a scored summary you can act on.

### SearchBot
Grid, spiral, and configurable-path automated area searching. Navigates a defined bounding box systematically, logs discovered items and structures, and stops on configurable trigger conditions.

> These are the modules in the Exploration & Hunting category. Each is independently configurable and many interconnect — BetterStashFinder feeds StashBotModule, Trails feeds TrailFollower and CoordPoppy, SmartActionBot can be driven by OllamaBotModule.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
