# Skylandia Module Catalog

> A reference across all Skylandia module categories.
> This is not a complete list — each category contains additional modules not documented here.
> Feature deep-dives are linked where they exist.

---

## 🧭 Exploration & Hunting

*Modules for finding what every other player missed.*

### Trails
The most advanced chunk classification system in any Minecraft client. Every loaded chunk is analyzed through up to 8 independent detection methods and assigned one of five forensic types: **NEW**, **OLD**, **BEING_UPDATED**, **OLD_GENERATION**, or **TICK_EXPLOIT**.

- **Palette Exploit Detection** — analyzes block palette ordering to distinguish freshly generated chunks from old ones (1.18+)
- **Legacy Chunk Update Detection** — marks chunks actively migrating from pre-1.17 generation as they load
- **Overworld/Nether/End Old Chunk Detectors** — version-specific forensic checks for each dimension
- **Real-Time Packet Detection** — processes chunk data packets as they arrive for immediate classification
- **Liquid & Block Update Exploit modes** — secondary heuristics for edge cases

Each chunk type is independently colored, logged, cached across sessions, and can fire Discord webhook alerts. Integrates with Xaero’s Minimap via XaeroPlus.

[→ Full deep-dive](features/trail-discovery.md)

---

### BetterStashFinder
Async chunk scanner that detects storage containers (chests, barrels, shulker boxes) and structures in every incoming chunk. Runs on a dedicated thread pool so detection never blocks the game.

**What it finds:**
- Storage blocks (flagged immediately with coordinate + Discord webhook)
- Villages — detected via iron golem and villager entity presence
- Trial Chambers — detected via trial spawner and Breeze entities
- Dungeons — spawner type analysis
- Custom structure rules via RuleManager

Player detection logs nearby players on a 5-minute interval. Auto-screenshots discovery moments. Creates Xaero waypoints on hit. Has a full custom GUI screen for managing discovered stashes.

---

### TrailFollower
Reads Trails’ chunk classifications in real time and autonomously navigates toward player-activity signals. Weighs incoming chunk data against configurable rules to determine the best bearing, executes the travel via AFKVanillaFly for long legs, and runs a fallback protocol (spiral / hold / return / stop) when the trail runs cold.

[→ Full deep-dive](features/trail-discovery.md)

---

### SmartActionBot
Natural language command executor and autonomous agent. Accepts a queue of movement, mining, and interaction commands. Parses them with a built-in stub and optional LLM integration. Simultaneously manages food/health, fights nearby enemies, and avoids revisiting positions. Designed to accept input from OllamaBotModule for a fully AI-driven field agent.

---

### CoordPoppy
Advanced minimap and reconnaissance surface. Subsystems include: **Randar exploit integration** (correlates RNG seed output with entity positions to locate players remotely), **RemoteEntityDetector**, **PlayerActivityTracker**, **LocationSpoofer**, **ChunkAnalyzer**, **TrailsIntegration** (overlays Trails classifications on the map), **TrailFollowerIntegration**, **SwarmIntegration** (multi-instance data sharing), and Discord webhook support.

---

### Other Exploration Modules

| Module | What it does |
|--------|--------------|
| **BaseFinder** | Detects and scores base-like terrain/entity signatures from chunk data |
| **CaveDisturbanceDetector** | Flags player-disturbed cave terrain: torches, unnatural block cuts, cleared sections |
| **StashBotModule** | Automated stash log: receives BetterStashFinder hits, writes log, creates waypoints, fires alerts |
| **TerrainAnalyzer** | Scores terrain for travel efficiency, PvP choke-points, and build strategy |
| **SearchBot** | Grid, spiral, and custom-path automated area searches with waypoint logging |
| **OldChunkNotifier** (render) | Alerts when you enter a historically loaded chunk |
| **SkyportalFinder** | Locates portals and portal frames in explored terrain |
| **RuleManager / SearchRule** | Defines custom detection rules for BetterStashFinder and SearchBot |

---

## ⚙️ Automation

*Modules that do things so you don’t have to.*

### DemonCrystal
End Crystal PvP engine. 60-tick movement prediction, 5 multi-crystal modes (Dual/Triple/Quad/Adaptive/Burst), 15 setting categories, anti-ghost placement, existence verification, anti-suicide and totem safety systems, emergency shutdown.

[→ Full deep-dive](features/demon-crystal.md)

---

### ChunkChestGrid
Builds a storage network by placing chests across a configurable grid of chunks (up to 50×50). Three routing strategies (Serpentine, Nearest-First, Adjacent Semi-Random), four placement patterns (Random, Grid, Corners, Center Focus), variable or fixed chest counts, expand-on-complete, shulker box restocking, and optional auto-craft from wood. Full render overlay shows current grid progress.

[→ See ShulkerTransport deep-dive for full context](features/shulker-transport.md)

---

### AIRraid
Aerial TNT bombing module. Only fires while elytra-flying above a configurable Y level and moving horizontally. Manages TNT and flint-and-steel hotbar slots automatically — switch, place, ignite, switch back — per placement. Zero manual slot management during a bombing run.

---

### AutoPromo (Wither Builder)
Automates summoning Withers. Scans a configurable radius for valid construction positions, builds the soul sand pattern, optionally names the spawned Wither with a name tag. Configurable delays, rotation assist, and single-shot mode. Useful for wither-based griefing or Nether Star farming workflows.

---

### ShulkerTransportModule
Two-account dimension logistics pipeline. Transporter + Commander role system, explicit confirmation handshake at each step, stasis chamber verification, item blacklist, encrypted SecureChat coordination, full rollback on failure.

[→ Full deep-dive](features/shulker-transport.md)

---

### AFKVanillaFly
Session-length AFK elytra flight. Locked altitude, velocity-aware firework timing, no input required. Used by TrailFollower for long travel segments.

---

### Other Automation Modules

| Module | What it does |
|--------|--------------|
| **Printer** | Automated schematic building |
| **SkylandiaHammer** | Large-area systematic mining |
| **Boomer** | TNT placement and detonation automation |
| **AutoEnchant** | Full enchanting workflow including table navigation and anvil combining |
| **EndDimensionProcessModule** | Automates End entry/exit sequence and dragon fight states |
| **SmartShulkerManager** | Tracks shulker fill levels, sorts contents, flags ready-for-transfer boxes |
| **AreaLoader** | Forces chunk loading in a defined region for build/automation prep |
| **TridentDupe / Tridentus** | Trident duplication and trident-based travel/combat aura |
| **Dualist** | Dual-wield combat flow automation |
| **AutoDropDupe / ChristeveDupe / ItemFrameDupe / duprexion** | Various duplication workflows |
| **MassRequester** | High-rate server request module |
| **CrashSuite** | Targeted crash utilities |
| **AutoSpeef** | Automated Spleef gameplay |

---

## 🛠️ Utility

*Quality-of-life and support modules that make everything else work better.*

### GrimEfly
Chestplate-based elytra flight via the bounce exploit. Your elytra **never takes durability**. Bounce mode with configurable pitch lock (default 90°), yaw lock, and custom yaw support. Obstacle Passer subsystem handles terrain interruptions. Baritone integration for ground-rerouting under low ceilings.

---

### ElytraSwap
Intelligent elytra lifecycle manager. Warns at configurable durability threshold. Auto-replaces broken elytra from inventory without interrupting flight. **Elytra Fixer** sub-group auto-repairs all elytras below a durability floor using Bottles o’ Enchanting. Handles held-elytra swapping for GrimEfly workflows.

---

### OllamaBotModule
Local LLM chat assistant inside Minecraft. Routes chat messages (prefix-triggered or respond-to-all) to a local [Ollama](https://ollama.com/) instance. 10-message rolling conversation memory. Configurable system prompt, model selection (auto-detected from Ollama), whitelist, and two-thread async execution so the game never waits.

---

### SecureChatModule
Client-side encrypted messaging layer. Encrypts outgoing chat and decrypts incoming for paired Skylandia clients on the same key. Also hosts custom chat filter rules. Backend for ShulkerTransportModule’s inter-account coordination channel.

---

### GrimDuraFirework
Conserves elytra durability under Grim anti-cheat by timing firework use to miss the server-side durability tick window. Required for long-distance flight on Grim-protected servers.

---

### AutoPromo
Wither builder. See Automation category.

---

### Other Utility Modules

| Module | What it does |
|--------|--------------|
| **Pitch40Util** | Locks pitch to 40° for optimal elytra height gain and velocity |
| **InfiniteTools** | Swaps tools before they break; keeps you working without interruption |
| **SignHistorian** | Archives and restores sign text; useful for documenting discoveries |
| **TrackerModule** | Logs and visualizes tracked player positions and movement over time |
| **BaritonePathing** | Baritone navigation as a Skylandia module with integrated settings |
| **JourneyRecorderModule** | AI-powered session narrative generation |
| **JourneyBookGUI** | In-game browser for saved journey stories |
| **AIStoryGenerator** | HuggingFace backend for story generation |
| **AutoLoginModule** | Automates server login commands on connect |
| **Numerology** | Coordinate analysis and seed-based math (Randar-compatible) |
| **BungeeSpoofer** | BungeeCord IP spoofing utility |
| **EnchantedAnvil** | Anvil interaction automation |
| **Firework** | Firework timing utility |
| **ServerScannerModule** | Network-level server scanning |

---

## 👁️ Render

*See more. Know more. Act faster.*

### CoordPoppy
Advanced minimap with Randar exploit, remote entity detection, player activity tracking, Trails/TrailFollower overlay, LocationSpoofer, ChunkAnalyzer, SwarmIntegration, and Discord webhook support. See Exploration section for full detail.

---

### HoleAndTunnelAndStairsESP
Terrain geometry analysis over a configurable chunk range (up to 1024 chunks). Detects holes (safe PvP spots), tunnels (navigable passages), and staircases (terrain transitions) simultaneously or in isolated modes. Y-range filtering, air-block-only mode, configurable processing rate (chunks per tick). Essential for PvP terrain reading at range.

---

### VanityESP
Highlights decorative world objects in a world scanner:
- **Item frames** — with special mapart outline color for frames containing maps
- **Banners** — all types, wall and floor
- **Signs** — for discovering player-left messages

Used by collectors and historians to find maparts, territory markers, and sign archives without walking the whole grid.

---

### DroppedItemESP
Keeps high-value dropped items visible at long range. Configurable item filter and distance. Prevents items from disappearing from view in chaotic situations.

---

### EntityClusterESP
Identifies and marks the **center of mass** of dense entity or player clusters at range. Useful for locating mob farms, player gatherings, or stash areas with a lot of container entities.

---

### Other Render Modules

| Module | What it does |
|--------|--------------|
| **PotESP** | Flags decorated pots and the items found inside |
| **MobGearESP** | Highlights mobs that picked up player-dropped loot |
| **CrystalPositionESP** | Visualizes optimal End Crystal placement positions in real time |
| **DamageNumbersModule** | Floating damage numbers displayed on hit — yours and incoming |
| **NerdVision** | Enhanced visibility in low-light and dark environments |
| **RoleTags** | Displays Lotus Clan role tags above recognized player heads |
| **OldChunkNotifier** | Alert overlay when you enter a historically loaded chunk |
| **ScreenBlackout** | Blackout overlay for privacy during screen sharing |
| **NoRender** | Selectively disables rendering categories for performance or clarity |
| **DemonCrystalHUD** | HUD overlay showing DemonCrystal state, target, and active mode |

---

## 🍩 Loukoumades (Contributed)

*Community-contributed modules maintained under the Loukoumades namespace.*

### TunnelBaseFinder
Anarchy-optimized base hunting via automated RTP and tunnel mining. Teleports to a configurable RTP region (EU_CENTRAL, NA, etc.), mines vertically down to a configurable Y level (default -60), then tunnels horizontally scanning for base signatures. Discord webhook alerts on hit. Configurable wait time between commands to match server rate limits.

---

### AutoSell
Automates item selling on servers with shop GUIs. Whitelist or blacklist mode — sells listed items or everything except listed items. Configurable item list and action delay. Re-opens the shop GUI automatically between sell cycles.

---

### RainNoti
Sends a notification when it starts raining in-game. Useful for farms and automation flows that depend on weather state.

> Loukoumades modules are community contributions. Quality and maintenance may vary; they are included as-is for members who find them useful.

---

## 🐍 Minescript Integration

### MinescriptIntegration
In-game Python script editor and launcher via [Minescript](https://minescript.net/). Write, edit, save, and execute `.py` scripts from the Minecraft GUI without opening an external editor. Scripts have access to the Minescript API for player movement, inventory, chat, block queries, and more. The integration includes a full service layer (`MinescriptService`, `RealMinescriptService`, `StubMinescriptService`) so Skylandia’s other modules can programmatically trigger script execution.

---

*[Back to README](../README.md) • [Website](https://unaveragetech.github.io/Skylandia/) • [Discord](https://discord.gg/MjMnsGhe8T)*
