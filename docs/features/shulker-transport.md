# 📦 ChunkChestGrid — Obfuscation Engine

> *Your enemy runs BetterStashFinder. They load in and their scanner lights up. Not because you were sloppy — because you deployed ChunkChestGrid.*

---

## What ChunkChestGrid Actually Is

ChunkChestGrid is an **obfuscation module** — the first of its kind in the Minecraft anarchy modding space. Its purpose is not storage. Its purpose is **denial of intelligence**.

Every stash-finding tool your enemies use — chest tracers, container scanners, BetterStashFinder-type modules, and manual coord-sharing — works on the same assumption: *chests in unexplored terrain are stashes*. ChunkChestGrid destroys that assumption. It autonomously carpets a region with a semi-random or precisely configured number of chests per chunk, across up to **50×50 chunks (2,500 total)**, until the scanner noise floor is so high that distinguishing a real stash from a planted false positive becomes computationally and operationally impossible.

**This is what it does to enemy intelligence:**
- A chest tracer scanning your region returns thousands of hits. Every one is valid. None of them matter.
- BetterStashFinder-type modules log every container they see. Their log is now 50,000 entries of useless data.
- Manual coord hunters who want to check "that cluster of chests" now have to check 2,500 clusters.
- Automated scanners running on alt accounts produce false positives at a rate that kills their signal-to-noise ratio permanently.

The module handles its own supply chain — when it runs out of chests, it opens your shulkers, crafts from planks, or chops trees — so it can **run indefinitely while you're offline**.

---

## The Obfuscation Configuration

### What Makes the Pattern Hard to Filter

The variable chest count per chunk is the key. You configure a `min-chests` and `max-chests` — ChunkChestGrid places a **random number within that range** in each chunk. This means:

- No two chunks have the same chest count
- There is no geometric regularity an automated filter can lock onto
- The distribution looks organic, not automated
- Raised `min-chests` creates denser noise fields; lower `max-chests` with high variability maintains plausible deniability about what is and isn't a real stash

### Placement Patterns

Four patterns control *where within each chunk* chests land:

| Pattern | Effect |
|---------|--------|
| `Random` | Chests at arbitrary positions within the chunk. Maximum pattern entropy — hardest to filter programmatically. |
| `Grid Pattern` | Regular grid within each chunk. Looks like someone organized a storage area. |
| `Chunk Corners` | Chests placed at corner positions. Matches common manual stash behavior. |
| `Center Focus` | Weighted toward chunk centers. Mimics organic build patterns. |

For maximum obfuscation, `Random` with high variability in chest count produces the least filterable output. For mimicking real player behavior, `Center Focus` or `Chunk Corners` with mid-range counts is more convincing.

### Routing Modes

| Mode | Behavior |
|------|----------|
| `Serpentine` | Row by row, reversing direction each pass — maximum coverage efficiency |
| `Nearest-First` | Always moves to the closest unfinished chunk — minimizes travel time in irregular terrain |
| `Adjacent Semi-Random` | Prefers adjacent chunks, randomizes within adjacency — produces the most natural-looking traversal signature |

`Adjacent Semi-Random` is the recommended mode for obfuscation deployments — if someone is watching movement data, the traversal pattern doesn't immediately flag as automated.

---

## The Autonomous Supply Chain

ChunkChestGrid runs a **7-state execution machine** that handles every supply failure without human intervention:

```
INITIALIZING
    ↓
MOVING_TO_CHUNK     ← Baritone or direct movement to next chunk
    ↓
PLACING_CHESTS      ← Places the configured (random) count per chunk
    ↓
    ↓ (inventory drops below refill threshold)
REFILLING_INVENTORY ← Opens shulker boxes, refills from them
    ↓
    ↓ (shulkers are empty)
CRAFTING_CHESTS     ← Opens any available crafting table, crafts from planks
    ↓
    ↓ (no planks or logs available)
COLLECTING_WOOD     ← Navigates via Baritone to nearest trees, chops them
    ↓
    ↓ (has logs)
CRAFTING_CHESTS     ← Crafts logs → planks → chests
    ↓
    ↓ (resupplied)
MOVING_TO_CHUNK     ← Returns to grid
    ↓
COMPLETED / ERROR
```

The wood-collecting path means ChunkChestGrid can **start with a completely empty inventory** and still build out a full 50×50 grid — it will simply go cut trees first. This makes it viable as a fire-and-forget deployment: log in, activate, log off. Come back to a region permanently poisoned against chest scanners.

---

## Scale and Coverage Settings

- **Grid size:** Up to 50×50 chunks — 2,500 chunks, potentially **50,000+ individual chest placements** at max density
- **Expand on complete:** When the grid finishes, automatically adds configurable rows and continues expanding the denial field
- **Per-chunk path optimization:** Minimizes walking distance *within* each chunk so placement is fast
- **Row validation:** After each row, re-checks the prior row for missed chunks and queues them for revisit
- **Skip completed:** Detects existing chests in a chunk and skips it — avoids redundant work on re-runs
- **Chunk timeout:** If stuck in a chunk for configurable seconds, moves on and returns later
- **Baritone integration:** Full Baritone pathfinding for terrain, water, buildings, and obstacles

---

## ShulkerTransportModule — Cross-Dimension Logistics

For the times you need to move the *real* stash — not the obfuscation field — ShulkerTransportModule coordinates two accounts through a structured pipeline with typed error handling and rollback:

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

**Rollback** — `TransportException` typed errors trigger rollback via `CoordinationManager`. If a step fails partway through, the system attempts to return both accounts to their pre-transfer state.

### SecureChat — The Coordination Channel

All inter-account communication runs over **SecureChatModule** — Skylandia's encrypted chat layer:

- **Three named channels** with independent passwords
- **Active channel switching** without reconfiguring
- **Message chunking** — splits messages at a configurable character limit so nothing exceeds chat limits
- **Message prefix** — identifies encrypted traffic to Skylandia clients
- **Discord webhook** — optionally logs channel passwords and history for audit

---

## SmartShulkerManager — Inventory Intelligence

Tracks shulker fill levels across your inventory, categorizes contents by item type, identifies deployment-ready vs depleted boxes, and queues them for the transport pipeline automatically. ChunkChestGrid uses this to know which shulkers contain chests and pull from them in the right order.

---

## The Combined Picture

You deploy ChunkChestGrid overnight. It blankets a 2,500-chunk region with tens of thousands of chests — random counts, organic placement patterns, all while handling its own supply chain from scratch if necessary. Enemy scanners load into the area and are immediately overwhelmed with noise. Your real stash, hidden somewhere in that region (or nowhere near it), is invisible. SmartShulkerManager tracks your actual inventory. When you need to move items cross-dimension, ShulkerTransportModule handles it through an encrypted two-account handshake. The infrastructure attacks your enemy's intelligence capability and protects your own simultaneously.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
