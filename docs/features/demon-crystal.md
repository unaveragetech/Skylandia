# 💎 DemonCrystal

> *Not a crystal aura. A combat operating system with 50 setting groups, a self-tuning AI, real-time strategy switching, and a CEV state machine that runs while you do nothing.*

---

## What You Need to Understand First

Most crystal clients have one loop: find target → place crystal → break crystal. DemonCrystal has **eight distinct attack strategies** that it switches between based on a live effectiveness scoring system:

| Strategy | What It Does |
|----------|--------------|
| `CRYSTAL_PLACEMENT` | Standard box-scan placement with damage prediction |
| `CEV_BREAKING` | Cev trap cycle: places trap block, places crystal, breaks the block, breaks the crystal, retraps |
| `CITY_MINING` | Mines the blocks around a target to expose crystal positions that normally couldn't exist |
| `SURROUND_BREAKING` | Breaks the target's own surround to open crystal opportunities |

A `FallbackLogic` system with states `EVALUATING → ATTEMPTING → SWITCHING → FAILED → SUCCESS` automatically rotates through strategies when the current one stops working — no manual reconfiguration mid-fight.

---

## The Self-Tuning System

This is the part that makes DemonCrystal different. It is not static.

The module maintains two live data structures:

**`PerformanceMetrics`** — tracked per session:
- Total damage dealt
- Crystals placed / broken
- Successful hits / total attempts
- Average damage-per-second
- Success rate

**`StrategyEffectiveness`** — tracked per attack strategy:
- Total damage from this strategy
- Times used / times succeeded
- Time spent per use
- Average effectiveness score (success rate × damage/second)

The `Self-Tuning & Optimization` setting group turns these metrics into automatic adjustments:
- **Rotation speed** adjusts based on placement accuracy
- **Placement range** adjusts based on placement success rate
- **Crystals per tick** reduces if placements trigger anti-cheat patterns
- **Burst cooldown** lengthens if the server struggles with the rate
- **Crystal count** (in multi-crystal mode) adjusts based on what the server can keep up with
- **Strategy selection** weights toward whichever attack type has the highest current effectiveness score

Enable `Demon Mode` and self-tuning together and the module *learns the fight*. It starts conservative, measures what works, and ramps aggression in real time.

---

## Movement Prediction

**`PredictiveData`** tracks per target:
- `lastPosition` — Vec3d
- `velocity` — Vec3d
- `predictedPosition` — Vec3d

Configurable up to 60 ticks of lookahead. The module places crystals where the target **will be**, accounting for their current velocity vector. Against a target running in a straight line at full speed, this means the crystal lands before they arrive.

Self-tuning adjusts prediction ticks based on measured accuracy — if predictions are consistently off, it reduces lookahead. If they're consistently accurate, it extends it.

---

## The CEV System in Detail

CEV (Crystal-Exploit-Vulnerability) is one of the highest-damage crystal PvP techniques. DemonCrystal's CEV state machine:

```
IDLE → TRAP_BLOCK → PLACE_CRYSTAL → BREAK_BLOCK → BREAK_CRYSTAL → RETRAP → COOLDOWN → IDLE
```

Each transition is automatic. The module places the trap block, immediately places a crystal on the obsidian adjacent to it, breaks the trap block to expose the target to the crystal, detonates, and retraps — all within the space of a few ticks. The `Cev Breaker` and `Anti-Cev Defense` setting groups let you both run CEV offensively *and* protect yourself from opponents running the same technique.

---

## The 50 Setting Groups

Here's every group and what it controls:

| Group | Purpose |
|-------|---------|
| 🔑 PvP Keybinds | Manual mining keybind — hold to allow block mining during placement |
| Core | Master switches: Demon Mode, Hyper Aggressive, Self-Tuning, Auto Gap |
| 🎯 Combat Targeting | Target range, priority (Closest/Health/Damage/Smart), foot targeting, face-place mode, face-place health threshold |
| ⚡ Combat Performance | Rotation mode/speed, max ops/tick, burst mode, burst duration/cooldown |
| 💎 Crystal Placement | Enable/disable, range, walls range, min damage, max self damage, crystals/tick, delay |
| 💥 Crystal Breaking | Enable/disable, range, walls break range, min damage break, crystals break/tick, delay |
| ⚔️ Advanced Crystal Combat | Advanced techniques |
| 📐 Placement Settings | Aggressive mode toggle |
| 💎 Multi-Crystal | Enable, max crystals, simultaneous placement count |
| 🪤 Trapping | Trap block placement for CEV setups |
| 🔮 Auto Pearl | Automatic ender pearl use for repositioning |
| 🧱 Block Placement | Obsidian/block auto-placement settings |
| ⛏️ Block Mining | Settings for city mining and surround breaking |
| 🛡️ Block Defense | Defensive surround block placements |
| 🏙️ City Mining | City target identification and mining patterns |
| 🏃 Movement Core | Basic movement behavior during combat |
| 🎮 Advanced Movement | Strafe modes (None/Low/Medium/High/Damage/Elytra), movement vectors |
| 🛡️ Movement Safety | Active-when modes (Always/InHole/OnGround/Sneaking/NotSneaking) |
| 🤖 Automation Systems | Full automation pipeline control |
| 🧠 AI & Self-Tuning | Aggressiveness multiplier, self-tuning master toggle |
| 🚨 Safety & Emergency | Anti-suicide threshold, emergency disable conditions |
| 🔧 Armor Mending | Mending rotation modes (None/LookDown/LookUp/LookAtFeet) |
| ⏰ Timing Settings | Fine-grained timing overrides |
| 🪜 Step Settings | Step assist behavior during combat |
| 🔄 Strafe Settings | Strafe boost levels, elytra strafe |
| 🪸 Burrow+ Settings | Burrow mode (Never/Always/Smart/Burrow/Trap) |
| 🕳️ Hole Fill Settings | Hole fill targeting (All/Smart/Target) |
| 🔄 Switching Settings | Item switching (Disabled/Silent/PickSilent/InvSwitch) |
| 🛡️ OffHand+ Settings | Off-hand item automation |
| ❤️ OffHand Health | Totem/gap health monitoring |
| 🎨 Render Settings | Crystal position rendering, colors |
| ⚡ Fast Use Settings | Fast item use timing |
| ⚓ Hole Anchor Settings | Snap to hole behavior |
| 🧲 Hole Snap Settings | Snap modes (Teleport/Move/Both/Yaw) |
| ⚡ Performance Settings | Processing limits per tick |
| 🎯 Targeting Settings | Extended targeting configuration |
| 🎨 Visual & Rendering | Full render pipeline settings |
| 🔧 Debug & Diagnostics | Debug output and diagnostics |
| 🛡️ Surround System | Surround mode (Auto/Manual/KeybindOnly), patterns (4-block/8-block extended) |
| 🧨 Cev Breaker | Offensive CEV configuration |
| 🧯 Anti-Cev Defense | Defensive counter to opponent CEV |
| 🛠️ Advanced City Mining | Extended city mining configuration |
| 🛡️ Inhibit System | Action inhibition conditions |
| 🧱 Anti-City Defense | Counter to opponent city mining |
| 🌫️ Air Placing | Crystal placement without ground contact |
| 🔄 Fallback Logic | Strategy rotation and fallback configuration |
| 🎯 Self-Tuning & Optimization | Full self-tuning behavior configuration |

---

## Rebreak Logic

The module maintains a live set of block positions it has mined (tracked with a 7-second expiry). If an opponent places a block back onto a position you just cleared, DemonCrystal detects it on the next tick and re-mines it. You can't be out-placed on positions you've already claimed in a fight.

---

## PlaceData Architecture (ThunderCrystal-Inspired)

Every possible placement position is evaluated as a `PlaceData` object:
```
BlockPos pos
double damage      → projected damage to target
double selfDamage  → projected damage to self
```

A spherical box scan (`getPossibleBlocksBox()`) evaluates every valid position within range. `filterBestPosition()` applies the damage thresholds, anti-suicide check, and max self-damage cap, then picks the globally best option. In multi-crystal mode, it then iterates remaining positions and places additional crystals in damage order up to the configured maximum.

This means DemonCrystal doesn't commit to the first valid position. It surveys every position simultaneously and picks the mathematically optimal placement on every single tick.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
