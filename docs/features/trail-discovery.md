# 🧭 Trail Discovery System

> *Log off. Come back to a map full of waypoints, coordinated across multiple accounts, with Discord alerts for every discovery.*

This is not a single module. It is a **four-module, multi-subsystem pipeline** where every component talks to every other. Trails classifies. TrailFollower navigates. AFKVanillaFly sustains. CoordPoppy maps, correlates, and coordinates the whole operation across multiple clients.

---

## Module 1: Trails — Chunk Forensics Engine

Every chunk that loads passes through Trails. It doesn't just flag "new" vs "old" — it assigns one of **five distinct forensic classifications**:

| Type | Meaning |
|------|---------|
| `NEW` | Generated post your world border. Nobody has been here. |
| `OLD` | Pre-dates the current world generation. Could be years untouched. |
| `BEING_UPDATED` | Actively migrating from <1.17 generation during load — you are watching the past become the present. |
| `OLD_GENERATION` | Legacy generation signature confirmed by block palette ordering. |
| `TICK_EXPLOIT` | Flagged via block update timing anomalies — a classic chunk-touch signature. |

Each type has **independent colors, notification toggles, Discord webhooks, and per-type render settings**. You can configure it so that *only* `TICK_EXPLOIT` chunks ping your Discord, for example.

### The Eight Detection Methods

You choose which detectors run. Each is independent and can be tuned:

| Method | How It Works |
|--------|-------------|
| **Palette Exploit** | The block palette inside a 1.18+ chunk section is ordered deterministically on first generation. If the order is wrong, the chunk is old or player-touched. This is the most reliable detector for modern servers. |
| **Legacy Chunk Update** | Marks chunks migrating from pre-1.17 generation in real time as they load. You can watch a 4-year-old world being converted, chunk by chunk. |
| **Overworld Old Chunk (Pre-1.17)** | Checks for block types above Y=0 that only exist in pre-Caves-and-Cliffs worlds. Finding them in a loaded chunk means it predates the 1.18 generation overhaul. |
| **Nether Old Chunk (Pre-1.16)** | Checks for the absence of warped/crimson/soul sand valley biome terrain. A missing Nether Update signature. |
| **End Old Chunk (Pre-1.13)** | Detects the `the_end` biome-only signature of pre-1.13 End generation. |
| **Real-Time Packet Detection** | Processes `ChunkDataS2CPacket` as it arrives. Classifications appear the moment a chunk loads, not on the next tick. |
| **Liquid Exploit** | Infers chunk generation age from flowing liquid patterns in terrain. |
| **Block Update Exploit** | Intercepts `BlockUpdateS2CPacket` and `ChunkDeltaUpdateS2CPacket` to flag recently-modified areas in otherwise old terrain. |

**XaeroPlus cross-reference** — when XaeroPlus is installed, Trails queries `PaletteNewChunks` and `OldChunks` modules for confirmation on ambiguous classifications.

**Session persistence** — chunk classifications survive log-off. The Saved Chunk Data and Cached Chunk Data setting groups control how long data lives and how it is serialized per-dimension.

**Per-type Discord pings** — each chunk type has a configurable Discord ping ID. You can @mention specific team members for specific discoveries.

---

## Module 2: TrailFollower — Autonomous Navigator

TrailFollower reads the Trails layer in real time and navigates toward it. Think of it as a strategist that *chases the signal*.

### What Makes It Different From "Just Flying Forward"

**Two movement modes** — `Simple` (reliable direct key presses) or `Smart` (Baritone pathfinding, handles obstacles, terrain, and block placements automatically).

**Two flight modes** — `PITCH40` (locks to 40° pitch, integrates with `Pitch40Util` for optimal elytra efficiency) or `VANILLA` (direct velocity control, no pitch constraints, higher raw speed).

**Two firework modes** — `VELOCITY` (fires a firework when speed drops below a configurable threshold) or `TIMED_DELAY` (fires at fixed intervals regardless of speed). Can also run entirely on velocity control with no fireworks required.

**POI Block Scanning** — you configure a list of *blocks of interest*. When any of those blocks appear in a newly loaded chunk, TrailFollower immediately weights that chunk's bearing more heavily. Hunting for a base that uses obsidian? Add obsidian to the POI list. It steers toward it.

**Destination Mode (Xaero Waypoint List)** — instead of trail-following, give it an ordered list of Xaero waypoint names. TrailFollower visits them in sequence, loops at the end if configured, and fires a Discord webhook at each one — with optional fields for waypoint name, completion percentage, distance to next, total waypoint count, coordinates, and timestamp.

**Anti-AFK movement randomization** — small variations in speed and direction make the movement pattern appear human-like to server monitoring.

**Debug overlays** — direction line, trail path lines with configurable colors, direction arrow, chunk data summary. You can watch the decision-making in real time.

### Trail End Behaviors

When the trail runs cold: configurable fallback — spiral outward, hold position, return to last known point, or clean shutdown.

---

## Module 3: AFKVanillaFly — The Sustain Engine

AFKVanillaFly doesn't just fly. It **integrates deliberately** with every other exploration module:

- **"Path Through Old Chunks"** — when enabled, AFKVanillaFly queries the Trails module directly and generates a flight path that *routes through old or player-touched chunks*. It's not just going somewhere. It's going somewhere deliberate.
- **"Respect AreaLoader"** — pauses automatically when AreaLoader is actively preloading a region, preventing conflicts.
- **Resource monitoring** — watches both firework count and elytra durability. Warns or auto-disables when either runs low, preventing a mid-flight crash 10,000 blocks from spawn.
- **Auto-land at final waypoint** — descends and lands cleanly instead of cutting flight and falling.
- **Auto-resume** — if interrupted (login, disconnect, knockback), resumes the path from where it stopped.
- **Obstacle avoidance** — detects blocks in the flight path ahead and pauses or reroutes rather than slamming into terrain.

---

## Module 4: CoordPoppy — The Intelligence Layer

CoordPoppy is a full reconnaissance surface built on top of everything else. It has 14 subsystem files.

### Randar Exploit Integration

You provide the server seed. `CoordPoppy` uses it to correlate the server's pseudorandom number generator output (observable via entity spawn positions) with predicted positions of *other* entities — including players. Without ever seeing them. Without them moving. The `RemoteEntityDetector` flags anomalies and the `PlayerActivityTracker` logs their presence history over time.

### Swarm Integration

CoordPoppy integrates with Meteor Client's Swarm system. Running two accounts? Three? All of them share their map data with each other every 10 seconds — chunk classifications, entity positions, waypoints. One account finds a stash. Every client on the swarm knows about it immediately.

### Full Subsystem List

| Subsystem | Role |
|-----------|------|
| `MapRenderer` | Custom minimap rendering layer |
| `BlockColorPalette` | Maps block types to configurable render colors |
| `ChunkAnalyzer` | Deep chunk pattern analysis beyond Trails' classification |
| `LocationSpoofer` | Masks real coordinates from server-side queries |
| `RemoteEntityDetector` | Flags entities that shouldn't exist based on activity patterns |
| `PlayerActivityTracker` | Builds a presence history log for observed players |
| `TrailsIntegration` | Overlays Trails chunk classifications on the map |
| `TrailFollowerIntegration` | Shows TrailFollower's current bearing and target on the map |
| `XeroIntegration` | Pulls data from and pushes to Xaero's Minimap |
| `SwarmIntegration` | Multi-instance data sharing via Meteor Swarm |
| `FilteringSystem` | Filters what entities, blocks, and events appear on the map |
| `SwarmMapData` | Data model for swarm-shared map state |

CoordPoppy has setting groups for: Map Appearance, Map Position, Stats UI Position, Proximity Detection, Mob Selection, Webhooks, Beacon Placement, Chunk Visualization, Entity Tracking, Advanced Mapping, Swarm Integration, Remote Scanning, Player Tracking, Filtering & Search.

---

## The Detection Subsystem (BetterStashFinder's Engine)

BetterStashFinder's structure detection runs through a dedicated architecture under `modules/exploration/detection/`:

| Detector | What It Finds |
|----------|---------------|
| `BedrockStaircaseDetector` | Bedrock staircase patterns — a classic anarchy base signature |
| `PistonDoorDetector` | Hidden piston doors in terrain — someone built a hidden entrance |
| `PortalFrameDetector` | Nether portal frame structures |
| `TunnelDetector` | Artificial tunnels carved through stone |
| `TunnelEntranceDetector` | The mouth of a tunnel, even when the tunnel continues beyond chunk range |
| `VillageAnomalyDetector` | A village that's been modified — signs of player habitation |
| `VillageHouseDetector` | Individual village building structural matches |
| `DungeonDetector` | Mossy cobblestone + spawner signature |
| `TrialChamberDetector` | Trial spawner + Breeze entity presence |

All of these feed into `DetectionManager` → `StructureDetectionManager` → BetterStashFinder's stash log → Xaero waypoints → Discord webhook.

---

## The Full Pipeline

```
Trails classifies every loaded chunk
    ↓ feeds bearing weights to
TrailFollower steers toward old/touched terrain
    ↓ hands long legs to
AFKVanillaFly sustains flight along a path through old chunks
    ↓ all three feed data to
CoordPoppy maps the operation, overlays Trails types,
    shows TrailFollower's bearing, runs Randar on known players,
    shares everything to swarm-connected accounts,
    fires Discord webhooks on discovery
```

You run this overnight. You wake up to a map covered in flagged chunks, structure detections, and Discord pings with coordinates.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
