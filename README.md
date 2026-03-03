<h1 align="center">🌌 Skylandia</h1>
<p align="center">
  <strong>A private Meteor Client addon for Minecraft anarchy and SMP.</strong><br/>
  Built for Lotus Clan. Crafted by <strong>Beelzebub4883</strong>.
</p>
<p align="center">
  <a href="https://unaveragetech.github.io/Skylandia/">Website</a> •
  <a href="https://discord.gg/bVcSMMMsbm">Discord</a> •
  <a href="#-getting-access">Get Access</a> •
  <a href="docs/modules.md">Module Catalog</a>
</p>

---

> Skylandia is a fully-modular Meteor Client addon built for the players who treat anarchy as a craft.
> The modules here solve problems others never attempted.

---

## Things Skylandia Does That You Haven't Seen Before

**ElytraSwap repairs your elytras in mid-air without landing.** It throws Bottles o' Enchanting upward at a configured angle, lets the XP orbs arc back down onto you, and repairs damaged elytras while you fly. When the bottles run out, it opens shulker boxes in your inventory to get more. Your elytra supply manages itself for the entire session.

**GrimEfly's Highway Obstacle Passer detects portal traps before you enter them.** On every chunk load, it scans incoming terrain for portal frame structures. If one is within threshold distance of your highway path, Baritone reroutes around it before you're ever in range — automatically.

**ChunkChestGrid is an obfuscation module — the first of its kind.** Its purpose is to negatively impact enemy stash scanners and tracers by autonomously blanketing a region in a semi-random or configured number of chests across up to 50×50 chunks. Every tool your enemy uses to find stashes — chest tracers, container scanners, BetterStashFinder-type modules — becomes worthless when there are tens of thousands of identically-structured false positives spread across 2,500 chunks. It handles its own wood supply, crafting, and routing without any input from you.

**DemonCrystal has a self-tuning AI that adjusts its own combat parameters during a fight.** It tracks damage-per-second, success rate, and strategy effectiveness in real time and modifies placement range, rotation speed, burst cooldown, and crystal count automatically based on what the server can handle and what's actually landing. It also runs eight distinct attack strategies (crystal placement, CEV breaking, city mining, surround breaking) and switches between them via a fallback system when the current one loses effectiveness.

**Journey Recorder's AI knows who you are.** You provide a user profile prompt (`"I'm a solo stash hunter, I value secrecy over efficiency"`) and a story theme (`"noir"`). The model writes your sessions from your character's perspective, in your genre. With incremental refinement enabled, it rewrites the story as you play so the final output is a cohesive narrative, not a log.

**CoordPoppy coordinates multiple Skylandia instances via Meteor's Swarm system.** Running two accounts? All of them share chunk classifications, entity positions, and Trails data with each other every 10 seconds. One account finds something — every client knows.

**TrailFollower has a POI block list.** Add any block type. When those blocks appear in a newly loaded chunk, TrailFollower steers toward it. Add obsidian. Add crying obsidian. Add ancient debris. It hunts whatever you tell it to hunt.

**BetterStashFinder's detection engine includes a PistonDoorDetector.** It scans for piston door patterns in loaded chunks — the classic hidden base entrance. It also runs BedrockStaircaseDetector, TunnelEntranceDetector, VillageAnomalyDetector, and six more.

**Trails fires a Discord @mention for specific chunk types.** Configure a Discord ping ID per chunk type. Only `TICK_EXPLOIT` chunks (the freshest player signatures) ping you? Done.

---

## Feature Deep-Dives

Four systems documented fully from source code — real settings, real integrations, real state machines:

| System | What It Covers |
|--------|----------------|
| [Trail Discovery System](docs/features/trail-discovery.md) | Trails (8 methods, 5 types), TrailFollower, AFKVanillaFly, CoordPoppy (14 subsystems), Detection architecture |
| [DemonCrystal](docs/features/demon-crystal.md) | 50 setting groups, self-tuning AI, CEV state machine, 8 attack strategies, PlaceData architecture |
| [Journey Recorder](docs/features/journey-recorder.md) | 20 recording categories, AI persona + genre, incremental refinement, ElytraSwap mid-air repair |
| [Shulker Transport & Obfuscation](docs/features/shulker-transport.md) | ChunkChestGrid obfuscation engine, ShulkerTransport pipeline, SecureChat encryption |

---

## Module Catalog

Skylandia has **six module categories**. The [full catalog](docs/modules.md) documents every module from source.

**🧭 Exploration & Hunting** — Trails, TrailFollower, AFKVanillaFly, CoordPoppy, BetterStashFinder (with 9 structure detectors), SmartActionBot (LLM+Baritone autonomous agent), BaseFinder, CaveDisturbanceDetector, StashBotModule, TerrainAnalyzer, SearchBot, SkyportalFinder.

**⚙️ Automation** — DemonCrystal (50 groups, self-tuning), ChunkChestGrid (obfuscation engine — first of its kind, 7-state autonomous supply chain, blankets 2,500 chunks with false-positive stash signatures), ShulkerTransportModule (10-file pipeline), AIRraid (aerial TNT), AutoPromo (Wither builder), Printer, SkylandiaHammer, Boomer, AutoEnchant, TridentDupe, Tridentus, Dualist, EndDimensionProcessModule, AreaLoader, SmartShulkerManager.

**🛠️ Utility** — GrimEfly (portal trap detection, obstacle passer, zero elytra durability), ElytraSwap (mid-air repair, shulker bottle extraction, auto-replace), OllamaBotModule (local LLM, 10-msg context, SmartActionBot integration), SecureChatModule (3-channel encrypted coordination), GrimDuraFirework, JourneyRecorderModule, Pitch40Util, InfiniteTools, SignHistorian, TrackerModule, BaritonePathing, Numerology, AutoLoginModule.

**👁️ Render** — CoordPoppy, HoleAndTunnelAndStairsESP (1024-chunk range), VanityESP (maparts/banners/signs), DamageNumbersModule, EntityClusterESP, PotESP, MobGearESP, DroppedItemESP, CrystalPositionESP, RoleTags, NerdVision, DemonCrystalHUD.

**🍩 Loukoumades (Community)** — TunnelBaseFinder (RTP→dig→tunnel hunt), AutoSell, RainNoti.

**🐍 Minescript** — MinescriptIntegration with programmatic triggering from any other module.

[→ Browse the full catalog](docs/modules.md)

---

## Dependencies

| Dependency | Required | Unlocks |
|------------|----------|---------|
| **Meteor Client** | ✅ | Core framework |
| **Fabric Loader + MC 1.21.4** | ✅ | Mod loader |
| **Xaero's Minimap + World Map + XaeroPlus** | Optional | Trails, BetterStashFinder, CoordPoppy, TrailFollower waypoints |
| **Baritone** | Optional | GrimEfly obstacle passer, ChunkChestGrid, TrailFollower Smart mode, SmartActionBot |
| **Minescript** | Optional | MinescriptIntegration |
| **Ollama (local)** | Optional | OllamaBotModule |
| **HuggingFace API token** | Optional | JourneyRecorderModule |

---

## 🔑 Access

Skylandia is **private**. Builds are individually authorized. The mod verifies your identity on every launch — if you're not on the list, nothing loads. How this works is not documented here.

---

## 📥 Getting Access

Access is earned through Lotus Clan membership or meaningful contribution — not purchased.

1. **Join the Discord:** [discord.gg/bVcSMMMsbm](https://discord.gg/bVcSMMMsbm)
2. **Participate:** Contribute to the clan, the codebase, or the community.
3. **Get reviewed:** Leadership extends access to approved members.
4. **Receive your build:** An authorized JAR with your account registered.

---

## ❓ FAQ

**Is the source code public?** No. Obfuscated authorized builds only.

**Which Minecraft version?** 1.21.4 on Fabric.

**Do I need all dependencies?** No — they unlock additional modules (Baritone, Xaero, Ollama, HuggingFace) but the core suite runs without them.

**My modules aren't loading.** Your username isn't authorized. Contact a Lotus Clan admin in Discord.

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
  <a href="https://discord.gg/bVcSMMMsbm">Discord</a> •
  <a href="docs/modules.md">Module Catalog</a>
</p>
