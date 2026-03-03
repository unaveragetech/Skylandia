<h1 align="center">🌌 Skylandia</h1>
<p align="center">
  <strong>A private, member-only Meteor Client addon for Minecraft anarchy and SMP.</strong><br/>
  Built for Lotus Clan. Crafted by <strong>Beelzebub4883</strong>.
</p>
<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a> •
  <a href="#-access--getting-in">Get Access</a>
</p>

---

> Skylandia is a fully‑modular Meteor Client addon born from the spirit of legendary anarchy repositories.
> It's designed for **exploration, automation, combat, and pushing the limits** of client‑side gameplay on
> anarchy and SMP servers. Whether you're a stash‑hunting veteran, a long‑haul traveler, or a tactician
> who demands the best tools — Skylandia is your Swiss Army knife.

---

## 🎯 What Skylandia Is

Skylandia is not a simple module pack. It's an evolving platform built around six core ambitions:

| Pillar | Description |
|--------|-------------|
| **Exploration Powerhouse** | Stash hunting, base detection, trail following, old chunk analysis, and large-scale scanning |
| **Automation Mastery** | Eliminate repetitive chores with smart bots, scripting, and session-length automation |
| **Enhanced Awareness** | Custom render layers, ESP overlays, and real-time combat readouts |
| **Add‑on Harmony** | Designed to work alongside Baritone, Xaero's Maps, Minescript, and more |
| **Innovation Hub** | A staging ground for experimental, bleeding-edge features |
| **Closed Community** | Private, access-controlled, and actively maintained for Lotus Clan members |

---

## 🛠 Feature Categories

Modules are organized into five in-game categories. Each module is configurable through the Meteor Client GUI and can be hotkey-bound.

---

### 🧭 Exploration & Hunting

The exploration suite is the heart of Skylandia — a collection of systems that work together to help you find, map, and reach anything in the world.

**Trail Discovery System** *(Trails + TrailFollower + AFKVanillaFly)*

The flagship exploration system. Three modules form an autonomous expedition pipeline:

- **Trails** — The analyst. Continuously classifies every loaded chunk using packet analysis and block state inspection, tagging them as new, old, modified, or legacy. Provides the intelligence layer for the entire system.
- **TrailFollower** — The strategist. Detects, analyzes, and pursues faint movement trails left behind by players. Uses directional weighting, chunk memory, and configurable search patterns to navigate toward old or player-touched chunks automatically.
- **AFKVanillaFly** — The pilot. Sustains hands-free high-velocity elytra flight for hours, automatically firing fireworks at boost-end and maintaining altitude, so the above two modules can work uninterrupted while you're AFK.

**Other Exploration Modules**

| Module | What it does |
|--------|-------------|
| **BaseFinder** | Detects and scores base-like structures using block and entity pattern recognition |
| **BetterStashFinder** | Advanced stash detection with loot-type filters and Xaero's World Map integration |
| **StashBotModule** | Automatically logs stash coordinates, sets waypoints, and fires alerts |
| **CaveDisturbanceDetector** | Flags signs of recent player activity — disturbed terrain, torches, placed blocks |
| **ActivatedSpawnerDetector** | Highlights active mob spawners in the surrounding area |
| **OldChunkNotifier** | Alerts you when you cross into a historically loaded chunk |
| **TerrainAnalyzer** | Profiles terrain for travel efficiency, build strategy, and PvP choke-points |
| **SearchBot** | Executes configurable search patterns (grid, spiral, random) with waypoint automation |

---

### 🤖 Automation

The automation suite handles the tedious, repetitive, and time-intensive parts of anarchy gameplay — so you can focus on what matters.

**Journey Recorder** *(AI‑Powered Story Generation)*

An AI‑powered storytelling system that records your gameplay and transforms it into narrative stories using HuggingFace AI models. It tracks movement, combat, item collection, dimension changes, and milestones, then generates readable story segments that chronicle your session. Stories can be exported and revisited.

**Shulker Transport System** *(Two-Account Coordination)*

An advanced multi-account logistics system for moving shulker boxes between the Overworld and End using coordinated stasis chamber teleportation. Two accounts operate in defined roles — Transporter and Commander — communicating over an encrypted chat channel, synchronizing pearl states, and executing item transfers with confirmation dialogs.

**DemonCrystal** *(Crystal PvP Automation)*

A 7,900-line combat automation engine built around End Crystal PvP. Covers:
- AI-enhanced target acquisition with movement prediction (1–60 tick lookahead)
- Configurable crystal placement patterns: surrounding, cross, diamond, trap formation, optimal damage
- Multi-crystal burst modes: dual, triple, quad, penta, adaptive
- Anti-suicide logic, emergency shutdown, totem safety, armor durability monitoring
- 15 organized feature categories with fine-grained control over every timing and threshold

**Other Automation Modules**

| Module | What it does |
|--------|-------------|
| **Minescript Integration** | In-game script editor and launcher for Minescript Python scripts |
| **AFKVanillaFly** | Session-length AFK elytra flight with auto-firework management |
| **AreaLoader** | Preloads large map regions for mapart or chunk preparation |
| **AutoEnchant** | Automates enchanting workflows at both anvils and enchanting tables |
| **AutomationModule** | General-purpose task automator for scripting repetitive actions |
| **AutoPortal** | Automates Nether portal traversal |
| **ChunkChestGrid** | Maps and populates chunk-based chest grids; includes adjacent semi-random traversal mode |
| **Boomer** | TNT placement and detonation automation |
| **Printer** | Automated block placement for schematic building |
| **SkylandiaHammer** | Automated large-area mining |
| **ShulkerTransportModule + SmartShulkerManager** | Shulker box inventory logistics and automated transport |
| **TridentDupe / Tridentus** | Trident duplication routines and trident-based travel / PvP automation |
| **AutoDropDupe / ItemFrameDupe / duprexion** | Experimental item duplication methods |
| **Dualist** | Dual-wield combat flow automation |
| **AIRraid** | Coordinated aerial attack automation |

---

### 🛡 Utility

| Module | What it does |
|--------|-------------|
| **GrimDuraFirework** | Conserves elytra durability by intelligently timing firework use under Grim's anti-cheat |
| **GrimEfly** | Chestplate-based vanilla elytra flight that prevents elytra durability loss |
| **ElytraSwap** | Automatically swaps between elytra and chestplate based on context |
| **Pitch40Util** | Locks pitch to 40° for optimal height gain and velocity |
| **SignHistorian** | Archives sign text and can restore it after a sign is broken or overwritten |
| **SecureChatModule** | Client-side encrypted messaging and custom chat filters |
| **AutoLoginModule** | Automates server login prompts and reconnect flows |
| **OllamaBotModule** | AI‑powered in-chat assistant via a local Ollama model |
| **BaritonePathing** | Exposes Baritone navigation as a configurable Skylandia module |
| **BungeeSpoofer** | Spoofs BungeeCord handshake data |
| **EntityFly** | Fly while riding entities |
| **InfiniteTools** | Prevents tool breakage by swapping at low durability |
| **JourneyRecorderModule** | In-game control panel for the Journey Recorder AI story system |
| **Numerology** | Coordinate and distance calculator utilities |
| **EnchantedAnvil** | Wiki-backed enchantment cost calculator |
| **ServerScannerModule** | Network-level server scanning utility |
| **TrackerModule** | Tracks and logs player positions and movement over time |

---

### 👁 Render

| Module | What it does |
|--------|-------------|
| **HoleAndTunnelAndStairsESP** | Highlights holes, tunnels, and staircase terrain — essential for PvP and navigation |
| **PotESP** | Flags decorated pots and the potion-effect items found inside |
| **MobGearESP** | Highlights mobs that have picked up player loot |
| **DroppedItemESP** | Keeps configurable high-value dropped items visible at long range |
| **EntityClusterESP** | Shows the center point of dense mob or player clusters |
| **VanityESP** | Highlights maparts and banners for collectors |
| **RoleTags** | Displays clan role tags above player heads |
| **CrystalPositionESP** | Visualizes optimal End Crystal placement positions for PvP |
| **DamageNumbersModule** | Floating real-time damage numbers in combat |
| **NerdVision** | Enhanced visibility in dark environments |
| **OldChunkNotifier** | Render-layer overlay marking historically loaded chunks |
| **CoordPoppy** | Coordinate display and management HUD |
| **ScreenBlackout** | Instantly blacks out the screen — useful for streaming control |

---

### 🏷 Loukoumades *(Clan-Specific)*

A private category reserved for Lotus Clan-specific modules and tools not published in the general feature list.

---

## 🔐 Access & Security

Skylandia is **member-only**. Access is not sold or distributed publicly. Every build is individually authorized through a multi-layered identity verification system that runs on every launch:

### How Authorization Works

**1. Embedded Whitelist**
The list of authorized usernames lives inside the JAR itself — not on a remote server. It cannot be modified by copying or editing local files.

**2. Per-Launch Regeneration**
On every launch, the whitelist is regenerated and cryptographically re-signed directly from the JAR. Local disk copies are always overwritten and never trusted as input.

**3. Cryptographic Signature Verification**
Each whitelist file is signed with a SHA-256 hash at write time. Before any module loads, the signature is verified. A missing, expired, or mismatched signature denies access to everyone — there is no silent fallback.

**4. UUID Verification**
For members with UUID mapping enabled, Skylandia verifies your Mojang UUID against the registered record — not just your username. This uses the official Mojang API with an automatic secondary fallback for reliability.

**5. Authenticated Load**
No module loads unless both the whitelist check and (if configured) UUID verification have passed for the current authenticated username. The mod cannot be loaded by detaching or bypassing the auth step.

> The specifics of the implementation are not documented here intentionally. The system is designed to degrade gracefully in all failure modes — access is always denied rather than accidentally granted.

---

## ⚙ Dependencies

| Dependency | Required | Notes |
|------------|----------|-------|
| **Meteor Client** | ✅ Required | Core framework |
| **Fabric Loader** | ✅ Required | Mod loader |
| **Minecraft 1.21.4** | ✅ Required | Target version |
| **Xaero's Minimap + World Map** | Optional | Unlocks BetterStashFinder, TerrainAnalyzer, TrailFollower, OldChunkNotifier |
| **Baritone** | Optional | Unlocks BaritonePathing, GrimEfly, AFKVanillaFly, SmartActionBot, TrailFollower, ChristeveDupe |
| **Minescript (Fabric)** | Optional | Unlocks MinescriptIntegration module |

---

## 📥 Installation

1. Ensure you have Meteor Client installed on Fabric for Minecraft 1.21.4.
2. Receive your authorized build JAR from a Lotus Clan admin (see **Getting Access** below).
3. Place the JAR in your `.minecraft/mods/` folder.
4. Launch Minecraft. On first launch the mod will verify your identity automatically.
5. Open the Meteor Client GUI to find Skylandia modules under their respective categories.

> **Note:** The public JAR distributed via this repo is the obfuscated community build. Module names and settings are preserved; internal implementation details are not readable from the distributed file.

---

## 🔑 Getting Access

Skylandia is a **reward for Lotus Clan members and meaningful contributors** — not a public release.

**Steps to get access:**

1. **Join the Discord:** [discord.gg/MjMnsGhe8T](https://discord.gg/MjMnsGhe8T)
2. **Participate:** Contribute to the clan, the codebase, or the community.
3. **Get reviewed:** Clan leadership reviews applicants and extends access to approved members.
4. **Receive your build:** Approved members receive an authorized JAR with their username registered.

---

## ❓ FAQ

**Is the source code public?**
No. The code is private. Only authorized, obfuscated builds are distributed.

**Which Minecraft version?**
Skylandia targets Minecraft 1.21.4 on Fabric.

**Which servers work best?**
Skylandia is optimized for anarchy and long-running SMP servers. Most modules function on any server; some automation features may be limited by server-side anti-cheat.

**Can I use it without Baritone / Xaero?**
Yes. Baritone and Xaero are optional. Modules that depend on them are loaded conditionally and silently disabled if the dependency is absent.

**My modules aren't loading — what do I do?**
Your username is likely not in the authorized whitelist. Join the Discord and reach out to an admin.

**Can I contribute?**
Yes. Contributions are one of the primary ways to earn access. Join the Discord and ask about open areas of work.

---

## 🐞 Known Limitations

- Some automation features (duplication routines, crash tools) are patched on most modern servers.
- TrailFollower and AFKVanillaFly require a stable server connection — frequent lag spikes may trigger the auto-disconnect safety system.
- The Minescript integration requires a separate Minescript Fabric mod install.
- OllamaBotModule requires a locally running Ollama instance.

---

## 🙌 Credits

| Role | Person |
|------|--------|
| **Author & Lead Developer** | Beelzebub4883 |
| **Co-developers** | ververybubbla, + contributors |
| **Community** | Lotus Clan members and testers |
| **Inspired by** | The pioneers of Minecraft anarchy modding and open-source client development |

---

> *Skylandia is a creator's toolkit — built to explore, automate, experiment, and push Minecraft's limits.*
> *Use responsibly. Enjoy the chaos.*

---

<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a>
</p>
