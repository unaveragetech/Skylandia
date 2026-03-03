<h1 align="center">🌌 Skylandia</h1>
<p align="center">
  <strong>A private Meteor Client addon for Minecraft anarchy and SMP.</strong><br/>
  Built for Lotus Clan. Crafted by <strong>Beelzebub4883</strong>.
</p>
<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a> •
  <a href="#-getting-access">Get Access</a> •
  <a href="docs/modules.md">Module Catalog</a>
</p>

---

> Skylandia is a fully-modular Meteor Client addon born from the spirit of legendary anarchy repositories.
> It’s designed for **exploration, automation, combat, and pushing the limits** of client-side gameplay.
> Whether you’re a stash-hunting veteran, a long-haul traveler, or a tactician who demands the best tools —
> Skylandia is your Swiss Army knife.

---

## Why Skylandia?

There are a lot of Meteor addons. Most bolt a handful of modules together and call it done.

Skylandia is different. The modules here solve problems at a level most clients don’t attempt:

- An exploration system that **autonomously hunts player trails across thousands of blocks** while you’re AFK
- A combat engine that **predicts target movement up to 60 ticks ahead** and places crystals where they’ll land
- An AI system that **turns your sessions into readable narrative stories** using live gameplay context
- A logistics pipeline that **coordinates two accounts across dimensions** with explicit safety handshakes
- A **Randar-exploit-powered minimap** that correlates RNG seeds with entity positions to locate players remotely
- An **in-game AI chat assistant** backed by your local LLM — ask it anything, get context-aware answers
- A chunk classification engine that tracks **5 distinct forensic chunk types** across 8 independent detection methods
- TNT **bombing runs from elytra altitude** with zero manual slot management
- An automated wither-summoning module that builds, places, and **names Withers** without touching a key

This is not a module pack. It’s a toolkit built by people who play anarchy seriously.

---

## Feature Deep-Dives

Some systems deserve more than a one-liner. These documents explain how the flagship modules actually work:

| System | Category | What it covers |
|--------|----------|-----------------|
| [Trail Discovery System](docs/features/trail-discovery.md) | Exploration | Trails + TrailFollower + AFKVanillaFly + CoordPoppy |
| [DemonCrystal](docs/features/demon-crystal.md) | Automation | Crystal PvP engine: prediction, modes, safety, companion modules |
| [Journey Recorder](docs/features/journey-recorder.md) | Utility | AI story generation + GrimEfly + ElytraSwap + OllamaBotModule |
| [Shulker Transport](docs/features/shulker-transport.md) | Automation | Two-account logistics + ChunkChestGrid + SmartShulkerManager |

---

## Module Catalog

Skylandia has **6 module categories** with dozens of modules total. The [full catalog](docs/modules.md) documents each category with detailed descriptions of key modules and a listing of everything else.

### Quick Category Overview

**🧭 Exploration & Hunting** — chunk forensics (5 types, 8 detectors), async stash scanning, Discord webhook alerts, Xaero waypoint integration, natural language navigation via Baritone + LLM, Randar exploit minimap.

> *Trails, BetterStashFinder, TrailFollower, SmartActionBot, CoordPoppy, BaseFinder, CaveDisturbanceDetector, StashBotModule, TerrainAnalyzer, SearchBot, SkyportalFinder, and more.*

**⚙️ Automation** — crystal PvP, aerial TNT bombing, wither spawning, multi-account dimension logistics, schema building, large-area mining, chunk-grid storage infrastructure, trident workflows.

> *DemonCrystal, AIRraid, AutoPromo, ChunkChestGrid, ShulkerTransportModule, AFKVanillaFly, Printer, SkylandiaHammer, Boomer, AutoEnchant, TridentDupe, Tridentus, EndDimensionProcessModule, Dualist, and more.*

**🛠️ Utility** — no-durability elytra flight (GrimEfly), intelligent elytra swap + auto-repair, local LLM chat assistant, encrypted inter-client messaging, Grim firework conservation, Baritone navigation, tool preservation.

> *GrimEfly, ElytraSwap, OllamaBotModule, SecureChatModule, GrimDuraFirework, Pitch40Util, InfiniteTools, SignHistorian, TrackerModule, BaritonePathing, JourneyRecorderModule, Numerology, AutoLoginModule, and more.*

**👁️ Render** — advanced Randar minimap with remote entity detection, hole/tunnel/staircase ESP (1024-chunk range), mapart and banner highlighting, damage numbers, mob gear detection, clan role tags.

> *CoordPoppy, HoleAndTunnelAndStairsESP, VanityESP, DroppedItemESP, EntityClusterESP, PotESP, MobGearESP, CrystalPositionESP, DamageNumbersModule, RoleTags, NerdVision, DemonCrystalHUD, and more.*

**🍩 Loukoumades (Community)** — contributed modules. RTP-and-tunnel base hunting, automated item selling, weather notifications.

> *TunnelBaseFinder, AutoSell, RainNoti.*

**🐍 Minescript** — in-game Python script editor and launcher with full Minescript API access and programmatic script triggering from other modules.

[→ Browse the full catalog with detailed descriptions](docs/modules.md)

---

## Dependencies

| Dependency | Required | Unlocks |
|------------|----------|---------|
| **Meteor Client** | ✅ | Core framework |
| **Fabric Loader + MC 1.21.4** | ✅ | Mod loader + target version |
| **Xaero’s Minimap + World Map + XaeroPlus** | Optional | Trails, BetterStashFinder, CoordPoppy, TrailFollower, OldChunkNotifier |
| **Baritone** | Optional | BaritonePathing, GrimEfly, AFKVanillaFly, TrailFollower, SmartActionBot |
| **Minescript** | Optional | MinescriptIntegration |
| **Ollama (local)** | Optional | OllamaBotModule |
| **HuggingFace API token** | Optional | JourneyRecorderModule / AIStoryGenerator |

---

## 🔑 Access

Skylandia is **private**. Builds are individually authorized. The mod verifies your identity on every launch — if you’re not on the list, nothing loads. How this works is not documented here.

---

## 📥 Getting Access

Access is earned through Lotus Clan membership or meaningful contribution — not purchased.

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

**Do I need all the optional dependencies?**  
No — they unlock additional modules but the core suite runs without them.

**My modules aren’t loading.**  
Your username isn’t authorized. Contact a Lotus Clan admin in Discord.

---

## 🙌 Credits

| Role | Person |
|------|--------|
| **Author & Lead** | Beelzebub4883 |
| **Co-developers** | ververybubbla, + contributors |
| **Community** | Lotus Clan members and testers |

---

> *Built to explore, automate, experiment, and push Minecraft’s limits.*  
> *Use responsibly. Enjoy the chaos.*

<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/MjMnsGhe8T">Discord</a> •
  <a href="docs/modules.md">Module Catalog</a>
</p>
