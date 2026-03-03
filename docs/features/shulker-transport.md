# 📦 Shulker Transport + Storage Infrastructure

> *One module builds the stash grid. Another fills it. Another repairs the wings that carry the goods. And when you need to move items across dimensions, two accounts coordinate through an encrypted channel with a structured safety handshake.*

---

## ChunkChestGrid — The Storage Builder

ChunkChestGrid doesn't just place chests. It runs a **full state machine** that handles every failure case automatically:

```
INITIALIZING
    ↓
MOVING_TO_CHUNK     ← Baritone or direct movement to next chunk
    ↓
PLACING_CHESTS      ← Places configured number of containers
    ↓
    ↓ (chest count drops below refill-threshold)
REFILLING_INVENTORY ← Opens shulker boxes in inventory, refills from them
    ↓
    ↓ (shulkers are empty too)
CRAFTING_CHESTS     ← Opens any available crafting table
    ↓
    ↓ (no planks/logs available)
COLLECTING_WOOD     ← Navigates via Baritone to the nearest trees and chops
    ↓
    ↓ (has logs)
CRAFTING_CHESTS     ← Crafts logs → planks → chests
    ↓
    ↓ (resupplied)
MOVING_TO_CHUNK     ← Back to the grid
    ↓
COMPLETED / ERROR
```

This means ChunkChestGrid will: run out of chests → open your shulkers to get more → if those are empty too → go find trees → chop them down → craft more chests → continue the grid. **Without you touching anything.**

### Grid Configuration

- Grid sizes up to **50×50 chunks** (2,500 chunks total)
- **Expand on complete** — when the entire grid is done, adds a configurable number of rows to each dimension and continues
- **Variable chest count** — place a random number of chests per chunk within a min/max range for natural-looking stash distribution
- **4 placement patterns** — Random, Grid Pattern, Chunk Corners, Center Focus
- **Per-chunk path optimization** — orders placements within a chunk to minimize walking distance inside it
- **Row validation** — after completing each row, ChunkChestGrid goes back and checks the prior row's placements and queues any missed chunks for a revisit
- **Chunk timeout** — if progress stalls in a chunk for configurable seconds, it moves on and comes back later
- **Skip completed** — detects existing chests in a chunk and skips over it

### Routing Modes

| Mode | Behavior |
|------|----------|
| `Serpentine` | Row by row, reversing direction each pass — maximum efficiency in a clean grid |
| `Nearest-First` | Always moves to the closest unfinished chunk — minimizes travel in irregular terrain |
| `Adjacent Semi-Random` | Prefers adjacent chunks, randomizes within adjacency — natural-looking traversal pattern |

### Baritone Integration

With `use-baritone` enabled, ChunkChestGrid delegates all movement to Baritone's pathfinder. It handles terrain, water, buildings, and obstacles. Without it, movement is direct — faster in open terrain, unreliable in complex environments.

---

## ShulkerTransportModule — Cross-Dimension Logistics

The ShulkerTransport system coordinates two accounts through the `automation/transport/` architecture — a fully modular pipeline with dedicated source files for state, configuration, coordination, and error handling:

| Component | Purpose |
|-----------|--------|
| `TransportState.java` | State machine definition |
| `TransportMode.java` | Transport mode enumeration |
| `TransportAction.java` | Individual action definitions |
| `TransportCondition.java` | Pre-condition checks for each action |
| `CommandSequence.java` | Ordered command sequences |
| `CoordinationManager.java` | Master coordinator between the two accounts |
| `InventoryManager.java` | Inventory validation and management |
| `StasisController.java` | Stasis chamber state management |
| `TransportConfig.java` | Persistent configuration |
| `TransportException.java` | Typed error handling and rollback |

### The Handshake Protocol

1. **Transporter** signals readiness via SecureChat
2. **Commander** validates both accounts' inventories against the configured item blacklist
3. **Commander** checks stasis chamber state via `StasisController`
4. If chamber state is invalid → **STOP**. The sequence does not continue.
5. **Commander** initiates pearl throw and chamber activation
6. **Commander** authorizes transfer
7. **Transporter** receives authorization over SecureChat and must confirm — **explicitly** — before execution
8. Transfer executes
9. Both accounts return to standby state

Timeout thresholds apply to every waiting step. If either account goes silent for longer than the configured timeout, the sequence halts and logs the failure point.

**Rollback** — `TransportException` typed errors trigger rollback logic via `CoordinationManager`. If a step fails partway through, the system attempts to return both accounts to their pre-transfer state.

### SecureChat — The Coordination Channel

All inter-account communication runs over **SecureChatModule** — Skylandia's encrypted chat layer.

SecureChat has:
- **Three named channels** with independent passwords — `general`, `party`, `raid`, or whatever you name them
- **Active channel switching** — change which channel you send/receive on without reconfiguring
- **Message chunking** — long messages are split into configurable-size chunks so they don't exceed chat limits
- **Message prefix** — a configurable prefix identifies encrypted messages so clients can distinguish them from regular chat
- **Discord webhook** — optionally logs channel passwords and message history to a Discord webhook for audit

The Transporter and Commander run on encrypted channel credentials that no other player on the server can see or decode.

---

## SmartShulkerManager — Inventory Intelligence

SmartShulkerManager runs alongside ChunkChestGrid and ShulkerTransportModule as a background housekeeping system. It tracks shulker fill levels across your inventory, categorizes contents by item type, identifies which shulkers are ready for deployment (full), which need to be emptied (depleted), and queues them for the transport pipeline automatically.

Instead of manually checking "which shulker has diamonds" — SmartShulkerManager knows, and surfaces that information at the moment it's needed.

---

## The Combined Picture

You set up a 20×20 chunk grid. ChunkChestGrid builds it — wood, crafting, routing, Baritone navigation, all automatic. SmartShulkerManager tracks what's stored where. ShulkerTransportModule moves items cross-dimension with encrypted account coordination. And your elytra? ElytraSwap repairs itself mid-air from shulkers in your inventory so you never land.

The infrastructure runs itself.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
