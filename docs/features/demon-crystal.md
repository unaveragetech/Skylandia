# 💎 DemonCrystal

> *End Crystal PvP, fully automated. Every placement, every break, every decision — handled.*

Crystal PvP is the highest skill ceiling in Minecraft combat. It rewards reaction speed, positioning discipline, crystal timing, and target prediction — simultaneously. Most players spend months developing muscle memory for it.

DemonCrystal puts that muscle memory in a module.

---

## What It Does

DemonCrystal automates the complete crystal PvP loop:

- **Target acquisition** using configurable priority rules — closest, lowest health, highest potential damage, least armor.
- **Movement prediction** up to 60 ticks ahead so crystals land where the player *will be*, not where they are now.
- **Crystal placement** in configurable geometric patterns: surrounding, cross, diamond, or pure damage maximization.
- **Burst breaking** with existence verification and anti-ghost logic — no wasted attacks on crystals already gone.
- **Dynamic target switching** when a better opportunity opens mid-fight.
- **Full safety suite** — anti-suicide, totem monitoring, durability checks, emergency shutdown.

---

## Multi-Crystal Modes

| Mode | What it does |
|------|--------------|
| **Dual** | Two crystals per sequence for pressure and spacing control |
| **Triple** | Three-point setups that corner targets |
| **Quad** | Maximum coverage, maximum damage, minimum time to pop |
| **Adaptive** | Picks count dynamically based on target health, distance, and open positions |
| **Burst** | Rapid-fire multi-crystal detonation sequence |

---

## Setting Categories (15 total)

DemonCrystal exposes 15 organized setting groups covering every aspect of the fight loop: target acquisition, placement geometry, break timing, burst behavior, anti-ghost, safety thresholds, totem handling, render options, and more. Most players use the defaults for general fights and tune individual thresholds for specific server anti-cheat profiles.

---

## Other Automation Modules

DemonCrystal is one of many automation modules in Skylandia’s combat and automation category:

### AIRraid
Aerial TNT bombing automation. Monitors your altitude and flight state — only activates above a configurable Y level (default 120) while elytra-flying and moving horizontally. Automatically switches to the TNT hotbar slot, places the block, then switches to flint-and-steel to ignite before returning to normal loadout. Lets you carpet-bomb targets while flying over them with zero manual slot management.

### AutoPromo (Wither Builder)
Fully automates summoning Withers. Scans a configurable horizontal/vertical radius for valid Wither construction positions, places soul sand in the correct T- or + pattern, and optionally names the spawned Wither using a name tag from your inventory. Settings include placement delay, block delay, rotation assist, and a `turn-off-after-one` mode. Useful for wither-based griefing workflows or farming Nether Stars without touching the keyboard.

### Boomer
TNT placement and detonation automation for large-scale destruction sequences. Configure placement patterns, ignition timing, and abort conditions.

### Printer
Schematic-based automated block placement. Feed it a schematic and a block supply and it builds the structure while you stand still or AFK.

### SkylandiaHammer
Large-area systematic mining automation with configurable area bounds and tool management.

### ChunkChestGrid
Places storage containers in a configurable grid across multiple chunks — up to 50×50 chunks, multiple routing modes, variable or fixed chests per chunk, expand-on-complete, and optional auto-craft from harvested wood. See the [full deep-dive](../features/shulker-transport.md) for logistics context.

### TridentDupe / Tridentus
Trident duplication pipeline and automated trident-based travel and combat. Tridentus extends this into a full aura/travel hybrid.

> The Automation category contains additional modules including ChristeveDupe, AutoDropDupe, ItemFrameDupe, duprexion, AutoSpeef, Dualist, Rotation utilities, and more.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
