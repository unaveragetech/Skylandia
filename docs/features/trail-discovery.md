# 🧭 Trail Discovery System

> *Autonomous exploration that hunts the past while you sleep.*

---

The Trail Discovery System is Skylandia's flagship exploration capability — a three-module pipeline that turns the chaos of an infinite Minecraft world into a navigable map of player history and forgotten terrain.

Most anarchy tools show you what's around you. This system **chases what was there before you**.

---

## The Three Modules

### Trails — The Analyst

Every chunk that loads gets classified. Not just "new" or "old" — Trails uses deep packet analysis, block-state inspection, and palette exploitation to assign each chunk a precise forensic type. Legacy generation signatures. Player-disturbed terrain. Freshly loaded borders. Update artifacts.

The result is a live intelligence layer that answers the question every stash hunter asks: *has a player ever been here?*

### TrailFollower — The Strategist

TrailFollower reads the Trails layer in real time and navigates toward it. When player-touched or historically loaded chunks appear, it weighs them against your configured rules and steers you on an optimal bearing — automatically.

It doesn't wander. It **hunts**.

When the trail runs cold, it doesn't stop — it executes a configurable search protocol: spiral outward, hold position and wait, return to the last known point, or shut down and preserve your position.

**Configurable behaviors include:**
- How much weight to give your current heading vs. new finds
- Memory of visited chunks to avoid doubling back
- Hard limits on trail deviation angle before abandoning a bearing
- When to hand off control to AFKVanillaFly for long legs

### AFKVanillaFly — The Pilot

Long-distance trail following requires flight you don't have to babysit. AFKVanillaFly maintains a locked altitude, monitors your velocity, and fires fireworks at exactly the right moment to sustain high-speed elytra flight indefinitely — without a single keypress from you.

TrailFollower hands the controls over when a long stretch is ahead. AFKVanillaFly takes it from there.

---

## What This Means in Practice

Set up the three modules, log out, and come back to a map full of waypoints.

The system will have followed trails across thousands of blocks, classified the chunks it passed through, avoided terrain it already covered, and logged everything it flagged — all while you were offline.

This is not a "hold W and hope" bot. It is an expedition commander that thinks about where to go next.

---

## Key Settings at a Glance

| Setting | What It Controls |
|---------|------------------|
| `visitedChunkInfluence` | Ignore, avoid, or prefer chunks you've already crossed |
| `trailEndBehavior` | What happens when the trail runs cold (spiral / wait / return / stop) |
| `flightMode` | Pitch40 for efficiency or Vanilla for open terrain |
| `maxTrailDeviation` | Hard angle limit before the system abandons a bearing |
| `autoDisconnect` | Safety cutoff if chunk load rate spikes unexpectedly |
| `startDirectionWeighting` | Bias toward continuing your initial heading for organic paths |

---

## Requirements

- **Trails** module (included in Skylandia)
- **Xaero's Minimap + World Map** — for on-map highlighting and waypoints
- **Baritone** — for ground-level pathing when elytra isn't viable

---

*Part of Skylandia's Exploration & Hunting category.*  
*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
