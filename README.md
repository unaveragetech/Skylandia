<h1 align="center">🌌 Skylandia</h1>
<p align="center">
  <strong>A private Meteor Client addon for Minecraft anarchy and SMP.</strong><br/>
  Built for Lotus Clan. Crafted by <strong>Beelzebub4883</strong>.
</p>
<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a> •
  <a href="#-getting-access">Get Access</a>
</p>

---

> Skylandia is a fully-modular Meteor Client addon born from the spirit of legendary anarchy repositories.
> It's designed for **exploration, automation, combat, and pushing the limits** of client-side gameplay.
> Whether you're a stash-hunting veteran, a long-haul traveler, or a tactician who demands the best tools —
> Skylandia is your Swiss Army knife.

---

## Why Skylandia?

There are a lot of Meteor addons. Most bolt a handful of modules together and call it done.

Skylandia is built differently. The modules here solve problems at a level most clients don't attempt:

- An exploration system that **autonomously hunts player trails across thousands of blocks** while you're AFK
- A combat engine that **predicts target movement up to 60 ticks ahead** and places crystals where they'll land
- An AI system that **turns your sessions into readable narrative stories** using live gameplay context
- A logistics pipeline that **coordinates two accounts across dimensions** with explicit safety handshakes

This is not a module pack. It's a toolkit built by people who play anarchy seriously.

---

## Feature Highlights

### 🧭 Trail Discovery System
*Autonomous exploration that hunts the past while you sleep.*

Three modules work as a pipeline: **Trails** classifies every loaded chunk using packet analysis and forensic techniques. **TrailFollower** reads that data in real time and navigates toward player-touched or historically significant terrain — automatically, with configurable search patterns for when the trail runs cold. **AFKVanillaFly** sustains hands-free high-velocity flight for session-length journeys so the other two modules can work uninterrupted.

Log out. Come back to a map full of waypoints.

→ [Full deep-dive: Trail Discovery System](docs/features/trail-discovery.md)

---

### 💎 DemonCrystal
*End Crystal PvP, fully automated. Every placement, every break, every decision — handled.*

DemonCrystal automates the complete crystal PvP loop — target acquisition with 60-tick movement prediction, placement in configurable geometric patterns, burst breaking with existence verification and anti-ghost logic, and dynamic target switching when a better opportunity opens. Five multi-crystal modes from Dual to Adaptive. Fifteen setting categories. Anti-suicide, totem safety, and an emergency shutdown that triggers before you're dead.

→ [Full deep-dive: DemonCrystal](docs/features/demon-crystal.md)

---

### 📖 Journey Recorder
*Your adventures, written by AI. Every session becomes a story worth reading.*

Journey Recorder tracks movement with directional and biome context, combat with location awareness, mining with depth and rarity tagging, and dimension transitions — then sends rich annotated session data to a HuggingFace AI model that generates readable narrative. Smart deduplication keeps the output coherent. Stories save to files you can read and keep.

→ [Full deep-dive: Journey Recorder](docs/features/journey-recorder.md)

---

### 📦 Shulker Transport System
*Two accounts. Two dimensions. One automated logistics pipeline.*

Coordinated multi-account inventory transfer between Overworld and End using stasis chamber teleportation. Two roles, a structured confirmation handshake, item blacklisting, encrypted inter-account communication, and full rollback logic if anything goes wrong at any step.

→ [Full deep-dive: Shulker Transport](docs/features/shulker-transport.md)

---

## Module Categories

### 🧭 Exploration & Hunting

| Module | What it does |
|--------|--------------|
| **BaseFinder** | Detects and scores base-like structures from block and entity patterns |
| **BetterStashFinder** | Advanced stash detection with loot-type filters and Xaero's World Map integration |
| **StashBotModule** | Logs stash coordinates, sets waypoints, fires alerts automatically |
| **CaveDisturbanceDetector** | Flags disturbed terrain, torches, and placed blocks — signs of a player |
| **ActivatedSpawnerDetector** | Highlights active mob spawners in the surrounding area |
| **OldChunkNotifier** | Alerts when you enter a historically loaded chunk |
| **TerrainAnalyzer** | Profiles terrain for travel efficiency, build strategy, and PvP choke-points |
| **SearchBot** | Grid, spiral, and custom-pattern automated area searches with waypoint logging |

### 🤖 Automation

| Module | What it does |
|--------|--------------|
| **Minescript Integration** | In-game script editor and launcher for Minescript Python scripts |
| **AFKVanillaFly** | Session-length AFK elytra flight with auto-firework management |
| **AreaLoader** | Preloads large regions for mapart or chunk preparation |
| **AutoEnchant** | Automates enchanting workflows at anvils and enchanting tables |
| **AutoPortal** | Automates Nether portal traversal |
| **ChunkChestGrid** | Maps and populates chunk-based chest grids; adjacent semi-random traversal mode |
| **Boomer** | TNT placement and detonation automation |
| **Printer** | Automated block placement for schematic building |
| **SkylandiaHammer** | Large-area automated mining |
| **TridentDupe / Tridentus** | Trident duplication and trident-based travel / PvP automation |
| **Dualist** | Dual-wield combat flow automation |

### 🛡 Utility

| Module | What it does |
|--------|--------------|
| **GrimDuraFirework** | Conserves elytra durability by intelligently timing firework use under Grim |
| **GrimEfly** | Chestplate-based vanilla elytra flight — elytra never takes durability |
| **ElytraSwap** | Automatically swaps between elytra and chestplate based on context |
| **Pitch40Util** | Locks pitch to 40° for optimal height gain and velocity |
| **SignHistorian** | Archives sign text and can restore it after a sign is broken |
| **SecureChatModule** | Client-side encrypted messaging and custom chat filters |
| **OllamaBotModule** | AI-powered in-chat assistant via a local Ollama model |
| **BaritonePathing** | Baritone navigation as a configurable Skylandia module |
| **InfiniteTools** | Prevents tool breakage by swapping at low durability |
| **ServerScannerModule** | Network-level server scanning utility |
| **TrackerModule** | Tracks and logs player positions and movement over time |

### 👁 Render

| Module | What it does |
|--------|--------------|
| **HoleAndTunnelAndStairsESP** | Highlights holes, tunnels, and staircase terrain — essential for PvP |
| **PotESP** | Flags decorated pots and the items found inside |
| **MobGearESP** | Highlights mobs that picked up player loot |
| **DroppedItemESP** | Keeps high-value dropped items visible at long range |
| **EntityClusterESP** | Shows the center of dense mob or player clusters |
| **VanityESP** | Highlights maparts and banners for collectors |
| **RoleTags** | Displays clan role tags above player heads |
| **CrystalPositionESP** | Visualizes optimal End Crystal placement positions |
| **DamageNumbersModule** | Floating real-time damage numbers in combat |
| **NerdVision** | Enhanced visibility in dark environments |

---

## Dependencies

| Dependency | Required | Unlocks |
|------------|----------|---------|
| **Meteor Client** | ✅ | Core framework |
| **Fabric Loader + MC 1.21.4** | ✅ | Mod loader + target version |
| **Xaero's Minimap + World Map** | Optional | BetterStashFinder, TrailFollower, OldChunkNotifier, TerrainAnalyzer |
| **Baritone** | Optional | BaritonePathing, GrimEfly, AFKVanillaFly, SmartActionBot, TrailFollower |
| **Minescript** | Optional | MinescriptIntegration module |

---

## 🔑 Access

Skylandia is **private**. Builds are individually authorized. The mod verifies your identity on every launch — if you're not on the list, nothing loads. How this works is not documented here.

---

## 📥 Getting Access

Access is earned through Lotus Clan membership or meaningful contribution — not purchased or distributed publicly.

1. **Join the Discord:** [discord.gg/MjMnsGhe8T](https://discord.gg/MjMnsGhe8T)
2. **Participate:** Contribute to the clan, the codebase, or the community.
3. **Get reviewed:** Leadership reviews and extends access to approved members.
4. **Receive your build:** An authorized JAR with your account registered.

---

## ❓ FAQ

**Is the source code public?**  
No. Only obfuscated authorized builds are distributed.

**Which Minecraft version?**  
1.21.4 on Fabric.

**Which servers?**  
Optimized for anarchy and long-running SMP. Most modules work anywhere; some automation may be limited by server-side anti-cheat.

**Do I need Baritone and Xaero?**  
No — they unlock additional modules but the core suite runs without them.

**My modules aren't loading.**  
Your username isn't authorized. Contact a Lotus Clan admin in Discord.

---

## 🙌 Credits

| Role | Person |
|------|--------|
| **Author & Lead** | Beelzebub4883 |
| **Co-developers** | ververybubbla, + contributors |
| **Community** | Lotus Clan members and testers |

---

> *Built to explore, automate, experiment, and push Minecraft's limits.*  
> *Use responsibly. Enjoy the chaos.*

<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a>
</p>
