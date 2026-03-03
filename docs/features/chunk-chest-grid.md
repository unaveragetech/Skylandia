# 📦 Chunk Chest Grid (CCG)

> *Deny the map. Fill it with noise. Make every tunnel and cavern look the same.*

---

Enemy scouting relies on landmarks — unique structures, empty spaces, identifiable terrain. The moment a rival faction explores your territory, they start building a mental map of it. CCG takes that map and corrupts it.

Chunk Chest Grid automates the deployment of a dense chest array across a configurable X/Z chunk grid, making large regions of terrain functionally indistinguishable and exploration operationally useless. Once activated, it handles all navigation, placement, inventory management, and supply logistics without manual input.

---

## What It Does

- **Builds a chunk grid** centered on your activation point — up to 50×50 chunks — and navigates each one in sequence.
- **Places chests per chunk** at a fixed or randomized count (configurable per-chunk min/max), using one of four spatial arrangements.
- **Manages its own inventory** by pulling chests from shulker boxes when running low, collecting wood, and crafting new chests on the fly.
- **Validates completed rows** and automatically queues any chunk that missed placements for a revisit, ensuring no gaps in coverage.
- **Expands automatically** when the grid is finished, if configured to do so.

---

## Why It Works As Anti-Exploration

A chest in isolation is a landmark. A thousand chests in uniform density is visual static.

| Scenario | Effect on enemy scouts |
|----------|----------------------|
| **Dense grid coverage** | No navigational anchor points — every corridor looks the same |
| **Cross-chunk saturation** | Map data captured by explorers becomes non-actionable noise |
| **Large-area deployment** | Scout teams can't efficiently survey the region in a reasonable timeframe |
| **Variable placement count** | Irregular patterns defeat scouts that know to look for uniform grids |

Enemies who explore a CCG-covered zone leave with data that tells them almost nothing useful about the actual layout of the territory.

---

## Placement Modes

Controls how chests are distributed within each chunk:

| Mode | Behavior |
|------|----------|
| **Grid** *(default)* | Evenly spaced grid inside the chunk; density scales with chest count |
| **Corners** | Four corners plus center — fast, predictable coverage |
| **Center Focus** | Dense cluster around the chunk's center point |
| **Random** | Seeded pseudo-random positions with enforced minimum spacing |

The **Random** and **Grid** modes both respect the `min-spacing` setting to prevent chest overlap.

---

## Chunk Routing Modes

Controls how the module traverses the grid between chunks:

| Mode | Behavior |
|------|----------|
| **Serpentine** *(default)* | Row-by-row, alternating direction each row to minimize backtracking |
| **Nearest-First** | Greedy nearest-neighbour ordering — always moves to the closest unfinished chunk |
| **Adjacent (Semi-Random)** | Prefers nearby chunks but occasionally jumps; harder to observe as a pattern |

---

## Automation Pipeline

CCG runs a full state machine so it never needs to stop for inventory management:

1. **Moving to Chunk** — Baritone navigates to the next target chunk, with timeout handling and auto-retry on path deviation.
2. **Placing Chests** — Walks to each planned position within the chunk, rotates, and places. Optimized walk order minimizes internal movement.
3. **Refilling Inventory** — When chest count drops below the threshold, places and empties a shulker box, then collects the empty shulker.
4. **Collecting Wood** — If no shulker boxes remain, uses Baritone to locate and harvest logs.
5. **Crafting Chests** — Crafts a crafting table from harvested logs, places it, opens it, and crafts chests until the inventory is restocked.
6. **Row Validation** — After completing each row (Serpentine mode), replays the previous row's placements and queues any chunk that came up short.

---

## Settings Reference

### General
| Setting | Default | Description |
|---------|---------|-------------|
| `grid-size-x` | 5 | Chunks in the X direction (1–50) |
| `grid-size-z` | 5 | Chunks in the Z direction (1–50) |
| `expand-on-complete` | off | Automatically add rows when all chunks are done |
| `expand-amount` | 1 | Rows added to each dimension per expansion |
| `variable-chest-amount` | off | Randomize chest count per chunk within a min/max range |
| `chests-per-chunk` | 4 | Fixed chest count per chunk (when variable is off) |
| `placement-mode` | Grid | Spatial arrangement of chests within each chunk |
| `skip-completed` | on | Skip chunks that already have chests |

### Movement
| Setting | Default | Description |
|---------|---------|-------------|
| `use-baritone` | on | Use Baritone for precise navigation |
| `forward-direction` | South | Direction the grid expands forward |
| `side-direction` | East | Direction the grid expands sideways |
| `routing-mode` | Serpentine | Chunk traversal order |
| `movement-timeout` | 30s | Max time to spend navigating to a chunk before skipping |

### Placement
| Setting | Default | Description |
|---------|---------|-------------|
| `placement-delay` | 3 ticks | Delay between each individual chest placement |
| `ground-only` | on | Only place on solid ground |
| `y-level` | 1 | Y offset from ground for placement |
| `min-spacing` | 3 | Minimum blocks between any two chests |
| `optimize-in-chunk-ordering` | on | Sort placement positions to minimize walking within each chunk |
| `validate-rows` | on | After each row, detect and queue under-filled chunks for revisit |
| `chunk-timeout` | 60s | Per-chunk time limit before moving on |

### Shulker Management
| Setting | Default | Description |
|---------|---------|-------------|
| `auto-refill` | on | Restock chests from shulker boxes |
| `refill-threshold` | 8 | Chest count that triggers a refill |
| `collect-shulker` | on | Pick up the emptied shulker box |

### Auto Crafting
| Setting | Default | Description |
|---------|---------|-------------|
| `auto-craft` | on | Craft chests when inventory is low and no shulkers remain |
| `craft-threshold` | 16 | Chest count that triggers a crafting run |
| `wood-to-collect` | 32 logs | Logs to harvest per crafting session |
| `crafting-timeout` | 120s | Max time allowed for a wood collection run |

### Render
| Setting | Description |
|---------|-------------|
| `render-chunk-bounds` | Draw chunk boundary outlines |
| `render-planned-chests` | Show planned (unplaced) chest positions in green |
| `render-placed-chests` | Show confirmed placements in cyan |
| `render-current-chunk` | Highlight the active target chunk in yellow |

---

## Operational Use Cases

**Territory denial** — Deploy across contested cave systems or tunnels connecting rival bases. Scouts who enter cannot efficiently relay usable positional data back to their faction.

**Staged obfuscation** — Cover the outer chunks surrounding your base first, creating a buffer zone where enemy scouting effort is absorbed before reaching anything sensitive. Use `expand-on-complete` to keep the perimeter growing.

**Post-raid recovery** — After a territory breach, rapidly redeploy the grid in compromised sections to degrade whatever intelligence the raiding party collected.

**Pattern disruption** — Use **Adjacent (Semi-Random)** routing with **variable chest counts** so the resulting coverage has no consistent structure that an experienced scout could map or reverse-engineer.

---
