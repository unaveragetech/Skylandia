# 📦 Shulker Transport System

> *Two accounts. Two dimensions. One automated logistics pipeline.*

Moving items between the Overworld and the End on an anarchy server is one of the most logistically demanding tasks in the game. It requires timing, precision, multi-account coordination, and no room for error.

The Shulker Transport System automates the entire process.

---

## How It Works

Two accounts operate in defined roles:

**The Transporter** holds the items and manages physical position in one dimension.  
**The Commander** coordinates the operation, validates inventories, and authorizes each step.

The system sequences through a structured handshake:

1. Transporter signals readiness
2. Commander validates both inventories against a configurable item blacklist
3. Commander initiates pearl throw and stasis chamber activation
4. Stasis controller verifies chamber state before proceeding
5. Commander authorizes the item transfer
6. Transporter confirms — explicitly — before execution
7. Transfer completes; both accounts return to standby

No step happens automatically without verification of the previous one.

---

## Safety Design

- Every transfer requires **explicit confirmation** before execution
- Items on the **blacklist** cannot be transferred — protects valuables from accidental movement
- If the stasis chamber state is invalid the sequence **stops and holds**
- Timeout thresholds on every coordinated step — if either account stops responding, the system halts
- Full **rollback logic** if a step fails partway through
- Inter-account communication runs over **SecureChat** — the encrypted Skylandia channel

---

## ChunkChestGrid — Building the Storage Network

Before you can transport items, you need somewhere to store them. **ChunkChestGrid** builds that infrastructure automatically.

ChunkChestGrid places storage containers in a systematic grid across a configurable area of chunks:

**Grid configuration:**
- X and Z grid sizes up to 50×50 chunks
- Expand-on-complete: when the grid is done, automatically adds more rows and continues
- Variable chest count per chunk (random within a min/max range) or fixed count

**Placement modes:**

| Mode | Behavior |
|------|----------|
| `Random` | Scattered placement within the chunk |
| `Grid Pattern` | Evenly spaced grid within each chunk |
| `Corners` | Places only at chunk corners |
| `Center Focus` | Concentrates toward the center of each chunk |

**Routing modes (how it moves between chunks):**

| Mode | Behavior |
|------|----------|
| `Serpentine` | Row by row, reversing direction each pass |
| `Nearest-First` | Always moves to the closest unprocessed chunk |
| `Adjacent Semi-Random` | Prefers adjacent chunks with randomized order |

**Inventory management:**
- Automatically refills from shulker boxes in your inventory when chests run low
- Optional auto-craft mode: collects wood, crafts chests, continues
- Tracks current grid state with a HUD overlay

ChunkChestGrid + ShulkerTransportModule is the full stash infrastructure pipeline — build the grid, fill it via automated transfers.

---

## SmartShulkerManager

A companion module to both ChunkChestGrid and ShulkerTransportModule. Manages the shulker box lifecycle independently: tracks fill levels, sorts contents by category, and flags shulkers ready for transfer or deployment.

---

## Other Automation Modules

The Automation category is Skylandia’s largest category. Beyond the transport and crystal systems:

### AreaLoader
Forces chunk loading in a defined area. Used before large builds, mapart preparation, or when you need a region pre-loaded before running other automation modules in it.

### AutoEnchant
Automates the enchanting workflow. Navigates to an enchanting table, selects the configured enchantment target, cycles through enchantments until the desired result appears, uses the enchanting table, then moves to an anvil to combine if needed.

### EndDimensionProcessModule
Manages the End dimension entry/exit sequence automatically. Handles the respawn screen acknowledgment, ender dragon fight states, and portal positioning for repeatable automated End runs.

> The Automation category also includes AutoDropDupe, ChristeveDupe, ItemFrameDupe, duprexion, CrashSuite, MassRequester, Dualist, AutoSpeef, Rotation utilities, and more. Each exists for a specific workflow that members of Lotus Clan have needed solved.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
