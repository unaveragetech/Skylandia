# 💎 DemonCrystal

> *End Crystal PvP, fully automated. Every placement, every break, every decision — handled.*

---

Crystal PvP is the highest skill ceiling in Minecraft combat. It rewards reaction speed, positioning discipline, crystal timing, and target prediction — simultaneously. Most players spend months developing muscle memory for it.

DemonCrystal puts that muscle memory in a module.

---

## What It Does

DemonCrystal automates the complete crystal PvP loop:

- **Identifies targets** using configurable priority rules — closest, lowest health, highest potential damage, least armor.
- **Predicts target movement** up to 60 ticks ahead so crystals land where the player *will be*, not where they are now.
- **Places crystals** in the optimal pattern for the situation — surrounding, cross, diamond, trap formation, or pure damage maximization.
- **Breaks crystals** with configurable timing, burst sequences, packet-level precision, and anti-ghost logic so you don't waste attacks on crystals that are already gone.
- **Switches targets dynamically** when a better opportunity opens mid-fight.
- **Protects you** with anti-suicide checks, totem safety logic, durability monitoring, and an emergency shutdown that triggers before you die.

---

## Multi-Crystal Modes

Single-crystal fighting is the floor. DemonCrystal supports:

| Mode | What it does |
|------|--------------|
| **Dual** | Two crystals per sequence for pressure and spacing control |
| **Triple** | Three-point setups that corner targets |
| **Quad** | Maximum coverage, maximum damage, minimum time to pop |
| **Adaptive** | Dynamically picks the count based on target health, distance, and available positions |
| **Burst** | Rapid-fire multi-crystal detonation sequence |

---

## Why It's Different

Most crystal automation modules are fast but dumb — they spam placement and hope something lands. DemonCrystal is purpose-built with:

- **Predictive targeting** that accounts for the tick delay between placement and explosion
- **Placement validation** with existence verification so it never tries to place on an already-occupied or invalid position
- **Pattern selection** that chooses the formation geometry based on the fight geometry at that moment
- **15 organized setting categories** with fine-grained control over every threshold, timing, and behavior

---

## Safety Systems

DemonCrystal will not kill you to kill someone else — unless you specifically configure it to.

- **Anti-suicide threshold** — stops attacking if your own projected damage exceeds your health margin
- **Totem safety** — adjusts aggression automatically when you or the target is holding a totem
- **Armor durability monitoring** — backs off when your protection is getting low
- **Emergency disable** — shuts the module down if the situation exceeds your configured safety limits

---

*Part of Skylandia's Automation category.*  
*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
