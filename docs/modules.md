# Skylandia Module Catalog

> Every module documented from source. Real settings. Real behaviors. Real integrations.
> This is not a feature list — it's an architecture guide.

---

## 🧭 Exploration & Hunting

### Trails
Chunk forensics engine. Eight detection methods, five classification types. Every loaded chunk is independently analyzed using palette exploit (block section ordering), legacy update detection, dimension-specific old-chunk signatures (separate detectors for Overworld/Nether/End), real-time packet processing, liquid exploit, and block update timing analysis. Results are cross-referenced against XaeroPlus modules when available.

Each of the five chunk types (`NEW`, `OLD`, `BEING_UPDATED`, `OLD_GENERATION`, `TICK_EXPLOIT`) has **independent** color rendering, notification toggle, Discord webhook URL, Discord ping ID, and persistence settings. You configure which chunk types alert you, which ones ping specific Discord members, and how long classifications persist between sessions.

[→ Full deep-dive with all 8 methods explained](features/trail-discovery.md)

---

### TrailFollower
Reads Trails classifications in real time. Steers toward player-touched or historically loaded terrain automatically.

**What makes it special:**
- **POI Block List** — add any block type. When those blocks appear in a newly loaded chunk, TrailFollower weights its bearing toward that chunk. Hunting obsidian-walled bases? Add obsidian. It steers toward it.
- **Destination Mode** — give it an ordered list of Xaero waypoint names. It visits them in sequence, loops if configured, fires a Discord webhook at each arrival (with fields: waypoint name, completion %, distance to next, total count, coordinates, timestamp).
- **Two movement modes** — Simple (direct key presses, reliable) or Smart (Baritone pathfinding, handles obstacles)
- **Two flight modes** — PITCH40 (locked 40° integration with Pitch40Util) or VANILLA (direct velocity, no constraints)
- **Two firework modes** — VELOCITY (speed-threshold-triggered) or TIMED_DELAY (interval-based)
- **Anti-AFK randomization** — small speed/direction variations to pass server movement monitoring
- **Debug overlays** — colored direction line, trail path, directional arrow, chunk data summary — watch the navigation decision in real time

[→ Full pipeline deep-dive](features/trail-discovery.md)

---

### AFKVanillaFly
Session-length AFK elytra flight. Notable integrations beyond basic flight:
- **Path Through Old Chunks** — queries Trails directly and routes through old/player-touched terrain
- **Respect AreaLoader** — pauses when AreaLoader is active to prevent resource conflicts
- **Auto-land** — descends and lands at the final waypoint instead of dropping
- **Auto-resume** — restarts path after interruptions
- **Obstacle avoidance** — detects blocks ahead, pauses or reroutes
- **Resource monitor** — warns/disables when fireworks or elytra durability are low
- **Anti-AFK movement randomization** for extended sessions

---

### CoordPoppy
14-subsystem reconnaissance layer. Seat of the Randar exploit integration — provide the server seed and the `RemoteEntityDetector` correlates RNG output with entity positions to locate players without line of sight. The `PlayerActivityTracker` builds a presence history over time.

**Swarm Integration** — uses Meteor's built-in Swarm system to share map data (chunk classifications, entity positions, waypoints, Trails overlay) with every other connected Skylandia instance every 10 seconds. Running multiple accounts? All of them see each other's discoveries in real time.

Full subsystem list: MapRenderer, BlockColorPalette, ChunkAnalyzer, LocationSpoofer, RemoteEntityDetector, PlayerActivityTracker, TrailsIntegration, TrailFollowerIntegration, XeroIntegration, SwarmIntegration, FilteringSystem, SwarmMapData.

Setting groups: Map Appearance, Map Position, Stats UI Position, Proximity Detection, Mob Selection, Webhooks, Beacon Placement, Chunk Visualization, Entity Tracking, Advanced Mapping, Swarm Integration, Remote Scanning, Player Tracking, Filtering & Search.

[→ CoordPoppy deep-dive within Trail Discovery](features/trail-discovery.md)

---

### BetterStashFinder
Async stash scanner backed by a dedicated detection architecture. Runs on a thread pool so chunk scanning never blocks the game. Per-chunk: scans all block entities for storage containers, then runs the detection pipeline in batches of 5 chunks per tick.

**Structure detectors included:**
- `PistonDoorDetector` — hidden piston entrances
- `BedrockStaircaseDetector` — classic anarchy base signatures
- `TunnelDetector` + `TunnelEntranceDetector` — artificial tunnels and their entrances
- `VillageAnomalyDetector` + `VillageHouseDetector` — modified or inhabited villages
- `PortalFrameDetector` — Nether portal frames
- `DungeonDetector` — mossy cobblestone + spawner
- `TrialChamberDetector` — trial spawner + Breeze entities

Player detection fires on a 5-minute interval with re-alert suppression. Auto-screenshots discoveries to Minecraft's screenshot folder. Creates Xaero waypoints on hit. Full custom GUI for managing the stash log.

---

### SmartActionBot
Natural language task executor. Maintains a command queue, parses commands (`"walk to 100 64 200"`), and executes through Baritone + input simulation. Simultaneously handles inventory management, food/health monitoring, basic combat, and visited-position tracking to prevent loops. LLM integration stub accepts input from OllamaBotModule for a fully AI-driven field agent.

---

### Other Exploration Modules

| Module | What it does |
|--------|--------------|
| **BaseFinder** | Scores chunk terrain/entity signatures for base-like patterns |
| **CaveDisturbanceDetector** | Flags player-disturbed cave terrain: torches, unnatural cuts, cleared sections |
| **StashBotModule** | Pipeline endpoint: receives BetterStashFinder hits, writes log, creates waypoints, fires alerts |
| **TerrainAnalyzer** | Scores terrain for travel efficiency, PvP choke-points, build suitability |
| **SearchBot** | Grid, spiral, custom-path automated area search with waypoint logging |
| **SkyportalFinder** | Locates portal frames in explored terrain |
| **OldChunkNotifier** | Alert overlay on entering a historically loaded chunk |

---

## ⚙️ Automation

### DemonCrystal
50 setting groups. A self-tuning combat AI that tracks performance metrics per session and per attack strategy and adjusts its own parameters in real time. Eight attack strategies with a `FallbackLogic` system that rotates when the current strategy loses effectiveness. Movement prediction up to 60 ticks. Box-scan placement that evaluates every possible position simultaneously and picks the mathematically optimal one on every tick. CEV state machine, city mining, surround breaking, rebreak protection, air placing, auto-gap, hole snap, burrow+.

[→ Full deep-dive](features/demon-crystal.md)

---

### ChunkChestGrid
**An obfuscation module — the first of its kind.** Its purpose is to negatively impact enemy stash scanners and tracers by autonomously blanketing a region in a semi-random or configured number of chests per chunk.

Every automatic stash-finding tool your enemies use assumes *chests in unexplored terrain = stashes*. ChunkChestGrid destroys that assumption at scale:
- Up to **50×50 chunks** (2,500 total) — potentially **50,000+ chest placements** at max density
- **Random chest count per chunk** (configurable min/max) — no geometric regularity for automated filters to detect
- **4 placement patterns** (Random, Grid, Corners, Center Focus) — each mimics different organic behavior
- **3 routing modes** (Serpentine, Nearest-First, Adjacent Semi-Random) — traversal pattern can look human
- **7-state autonomous supply chain** — runs out of chests → opens shulkers → crafts from wood → chops trees → continues; operates indefinitely overnight
- **Expand on complete** — keeps growing the noise field after finishing the initial grid
- Row validation, per-chunk timeout, skip-completed, Baritone navigation

[→ Full deep-dive with obfuscation strategy and state machine](features/shulker-transport.md)

---

### ShulkerTransportModule
Two-account cross-dimension logistics via stasis chambers. Full modular pipeline: `CoordinationManager`, `StasisController`, `InventoryManager`, `CommandSequence`, `TransportCondition`, `TransportAction`, `TransportException` with rollback. Explicit confirmation handshake, item blacklist, encrypted SecureChat inter-account channel, per-step timeouts, typed error rollback.

[→ Full deep-dive](features/shulker-transport.md)

---

### AIRraid
Aerial TNT bombing. Only fires when elytra-flying above a configurable Y level and moving horizontally — won't accidentally bomb your own base when walking. Manages TNT hotbar slot and flint-and-steel hotbar slot independently: switches to TNT → places → switches to igniter → ignites → switches back. Per-bomb. Zero manual hotbar management in a bombing run.

---

### AutoPromo (Wither Builder)
Fully automates Wither summoning. Scans a configurable horizontal/vertical radius for valid construction positions, places the soul sand T/+ pattern, optionally names the spawned Wither with a name tag from inventory. `block-delay` (0 = instant placement), `wither-delay` (gap between multi-wither builds), rotation assist, single-shot mode. Visual render overlay shows planned construction positions in configurable colors.

---

### SmartShulkerManager
Tracks shulker fill levels, categorizes contents, identifies deployment-ready vs depleted boxes. Surfaces the right shulker at the right moment for ChunkChestGrid, ShulkerTransportModule, and ElytraSwap's Elytra Fixer.

---

### Other Automation Modules

| Module | What it does |
|--------|--------------|
| **Printer** | Automated schematic building |
| **SkylandiaHammer** | Large-area systematic mining |
| **Boomer** | TNT placement and detonation automation |
| **AutoEnchant** | Enchanting workflow: table navigation, enchantment selection, anvil combining |
| **EndDimensionProcessModule** | Automates End entry/exit sequence and dragon fight states |
| **AreaLoader** | Forces chunk loading in a defined region for build/automation preparation |
| **TridentDupe / Tridentus** | Trident duplication + trident-based travel and combat aura |
| **Dualist** | Dual-wield combat automation |
| **AutoDropDupe / ChristeveDupe / ItemFrameDupe / duprexion** | Various duplication workflows |
| **MassRequester** | High-rate server request utility |
| **CrashSuite** | Targeted crash utilities |
| **AutoSpeef** | Automated Spleef gameplay |

---

## 🛠️ Utility

### GrimEfly
Chestplate-based elytra flight via the bounce exploit. Your elytra **never takes durability hits**. When you activate GrimEfly, it auto-equips a chestplate (fixing a reconnect bug where you join wearing the elytra).

**Highway Obstacle Passer** — the unique feature. When `highwayObstaclePasser` is enabled, Baritone handles terrain interruptions automatically:
- Configurable start position (`(0,0)` default, custom for ringroads)
- `awayFromStartPos` — whether to path toward or away from origin
- `avoidPortalTraps` — scans incoming chunks for portal trap structures and reroutes Baritone around them before you enter range
- `portalScanWidth` — how wide an area to scan perpendicular to the highway axis
- `portalAvoidDistance` — how far ahead to start the reroute
- `baritoneOffset` — fine-tune where Baritone places its goals relative to your position
- `targetY` — lock the bounce Y level for consistency in tunnel sections
- `Jump Delay` — control speed in 1×2 tunnels by varying bounce timing
- **Stuck detection** — if you stop moving, the module toggles itself off and on to reset state

Portal trap detection happens on `ChunkDataEvent` — before you're close enough to enter one.

---

### ElytraSwap
Intelligent elytra lifecycle manager with four sub-systems:

1. **Warning** — durability threshold alert
2. **Auto-Replace** — swaps in a fresh elytra from inventory when durability drops below a second threshold, mid-flight, without you noticing
3. **Elytra Fixer** — automatically repairs all elytras below a durability floor using Bottles o' Enchanting. When bottles run out, opens nearby shulker boxes (configurable scan range) or opens inventory shulkers to extract more. Your elytra supply is self-sustaining.
4. **Mid-Air Fixing** — repairs elytras while flying:
   - **Platform mode** — places a temporary block above or below you, lands on it, fixes, auto-breaks platform. `auto-break-platform` removes the evidence.
   - **Bottle-throw mode** — throws bottles upward at a configurable angle. XP orbs arc overhead and fall on you. Configure throw angle, bottles before collecting, collect duration in ticks.
   - `auto-trigger-mid-air-fix` — fires automatically when broken elytra count hits threshold
   - SafeWalk toggle prevents falling off your own platform

[→ Full ElytraSwap context in Journey Recorder deep-dive](features/journey-recorder.md)

---

### OllamaBotModule
Local LLM chat assistant via Ollama (`localhost:11434`). Trigger prefix (default `!ask`) or respond-to-all mode. 10-message rolling conversation context. Configurable system prompt, model (auto-detected from Ollama), whitelist of allowed users. Two-thread executor — never blocks the game waiting for a response. `refresh-models` queries Ollama live and populates available models. Can be used as the input source for SmartActionBot's command queue for a fully AI-driven autonomous agent.

---

### SecureChatModule
Client-side encrypted messaging layer. Three named channels with independent passwords. Active channel switching without reconfiguration. Long message chunking at a configurable character limit. Message prefix to distinguish encrypted messages from regular chat. Discord webhook for password and message history logging. Used by ShulkerTransportModule as the inter-account coordination channel.

---

### GrimDuraFirework
Conserves elytra durability under Grim anti-cheat by timing firework use to miss the server-side durability tick window. Required on Grim-protected servers for untouched elytra during long sessions.

---

### JourneyRecorderModule
20-category session recorder. Configurable in every dimension. AI narrative generation via HuggingFace with user profile personalization, story theme/genre selection, incremental refinement mode, auto-integration of segments, Discord webhooks for both story and raw data. Smart deduplication with similarity window and aggregate counting. In-game book GUI with configurable cover style and position.

[→ Full deep-dive](features/journey-recorder.md)

---

### Other Utility Modules

| Module | What it does |
|--------|--------------|
| **Pitch40Util** | Locks pitch to 40° for optimal elytra height gain |
| **InfiniteTools** | Swaps tools before breaking — keeps the workflow uninterrupted |
| **SignHistorian** | Archives and restores sign text — documents the world's history |
| **TrackerModule** | Logs and visualizes tracked player positions over time |
| **BaritonePathing** | Baritone navigation exposed as a Skylandia-integrated module |
| **JourneyBookGUI** | In-game paginated story browser |
| **AIStoryGenerator** | HuggingFace API backend for journey narrative generation |
| **AutoLoginModule** | Automates server login commands on connect |
| **Numerology** | Coordinate analysis and seed-based math (Randar-compatible) |
| **BungeeSpoofer** | BungeeCord IP spoofing |
| **EnchantedAnvil** | Anvil interaction automation |
| **Firework** | Firework timing utility |
| **ServerScannerModule** | Network-level server scanning |

---

## 👁️ Render

### CoordPoppy
See Exploration section. Render category because it overlays on the minimap, but it does far more than render.

---

### HoleAndTunnelAndStairsESP
Terrain geometry analysis for PvP. Configurable render distance up to 1024 chunks. Four detection modes: holes, tunnels, stairs, or all simultaneously. Y-range filtering (min/max offset from world limits). Air-block-only mode for stricter hole detection. Configurable chunks-per-tick processing rate to balance performance. Independent color settings for holes, tunnels, and staircases.

---

### VanityESP
Maps the world's decorative layer:
- **Item frames** — highlighted in configurable color; frames containing maps get a separate mapart outline color
- **Banners** — wall and floor, all types
- **Signs** — highlights player-left messages

Used by collectors and historians to find maparts, territory markers, and sign archives without grid-walking.

---

### DamageNumbersModule
Floating damage numbers on every hit — yours and incoming. Real-time combat feedback without leaving the game.

---

### EntityClusterESP
Computes and marks the center of mass of dense entity or player clusters at range. Cluster size thresholds configurable. Useful for locating mob farms, player gatherings, or high-entity stash areas.

---

### Other Render Modules

| Module | What it does |
|--------|--------------|
| **PotESP** | Flags decorated pots and contents |
| **MobGearESP** | Highlights mobs wearing player-dropped loot |
| **DroppedItemESP** | Keeps high-value drops visible at long range |
| **CrystalPositionESP** | Optimal crystal placement positions in real time |
| **RoleTags** | Clan role tags above recognized player heads |
| **NerdVision** | Enhanced low-light visibility |
| **DemonCrystalHUD** | DemonCrystal state, current strategy, target, active mode |
| **OldChunkNotifier** | Alert when entering a historically loaded chunk |
| **ScreenBlackout** | Blackout overlay for screen sharing |
| **NoRender** | Selective render category disabling |

---

## 🍩 Loukoumades (Contributed)

### TunnelBaseFinder
Anarchy base hunting via RTP + mining. Teleports to a configurable RTP region (EU_CENTRAL, NA, etc.), mines vertically to a configurable Y level (default -60, configurable to -64→80), then tunnels horizontally scanning for base signatures. Discord webhook on hit. Configurable wait between commands to match server rate limits. `vertical-mine` toggle for disabling the dig-down phase on flat terrain.

### AutoSell
Automates item selling in GUI-based shop systems. Whitelist mode (sell only listed items) or blacklist mode (sell everything except listed items). Configurable sell delay (0–20 ticks). Re-opens shop GUI between cycles automatically.

### RainNoti
Weather-state notification for farm automation timing.

---

## 🐍 Minescript Integration

### MinescriptIntegration
In-game Python script editor and launcher. Write, edit, save, and execute `.py` scripts from the Minecraft GUI. Full Minescript API access: player movement, inventory manipulation, chat, block queries. Service architecture: `MinescriptService` interface, `RealMinescriptService` (live), `StubMinescriptService` (testing). Other Skylandia modules can call `MinescriptServiceFactory.get()` to trigger script execution programmatically — making every module in Skylandia scriptable.

---

*[Back to README](../README.md) • [Website](https://unaveragetech.github.io/Skylandia/) • [Discord](https://discord.gg/bVcSMMMsbm)*
