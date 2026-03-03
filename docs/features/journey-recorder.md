# 📖 Journey Recorder

> *Your sessions become stories. Your character has a voice. The AI knows who you are, what you care about, and writes in your genre.*

---

## What It Records

Journey Recorder is not a position logger. It tracks **contextually enriched events** across 20 independently toggleable recording categories:

| Category | What Gets Logged |
|----------|------------------|
| **Movement** | Direction, biome, height, distance from session origin — not just "moved 200 blocks" but *where, through what, from how far* |
| **Flying** | When elytra flight starts and stops, altitude context |
| **Sprinting** | Distance sprinted with terrain context |
| **Swimming** | Swimming distance with water type |
| **Blocks Broken** | Type, depth, with *valuable block highlighting* (diamonds, ancient debris, amethyst) |
| **Blocks Placed** | Type and location |
| **Rare Items** | Item pickups flagged as rare/valuable get separate treatment |
| **Combat** | Every kill and death with location and cause |
| **PvP Specifically** | Player kills logged separately from mob kills |
| **Mob Kills** | Hostile mob kills with accumulated session count |
| **Boss Kills** | Ender Dragon, Wither — always preserved regardless of deduplication |
| **Deaths** | Cause of death and coordinates |
| **Crafting** | Key crafting events |
| **Dimension Changes** | Every portal, End gateway, Nether crossing — with entry and exit coordinates |
| **Biome Changes** | Every new biome entered, readable name (not internal ID) |
| **Structures** | Entering villages, temples, dungeons, other structures |
| **Villages** | Village discovery with villager/golem count |
| **Distance Stats** | Total distance from session start — fed to AI for narrative scale |
| **Time Stats** | Total time played in session |
| **Milestones** | Achievement-style tracking |

---

## The AI Layer — More Than "Generate a Story"

### You Give It Your Character

The `user-profile-prompt` setting is a free-text field: *"I'm a solo anarchy player who builds stashes in the deep ocean and never PvPs unless provoked. I value secrecy over efficiency."* The AI includes this in its prompt. The story it generates is written from **your character's perspective**, not a generic narrator's.

### You Give It a Genre

The `story-theme` setting is another free-text field: `"noir"`, `"whimsical"`, `"horror"`, `"military report"`. The model writes in that register. A night of combat mining in the deep slate reads differently as noir vs. military report vs. horror.

### It Writes While You Play

**Incremental refinement mode** changes the generation pipeline entirely. Instead of waiting until the end of a session:

1. Every `refinement-batch-size` actions, the model generates an intermediate narrative segment
2. If `auto-integrate-segments` is enabled, the model then **rewrites the entire story so far** to integrate the new segment — adjusting pacing, resolving narrative gaps, maintaining voice consistency
3. At the end, the story is already cohesive — not a list of events stapled together

Each refinement pass has its own configurable temperature and max tokens, separate from the main generation settings.

### Discord Webhooks for Every Story

- `webhook-on-story` — fires when a story segment is generated, sends the narrative text to Discord
- `webhook-on-raw-data` — also sends the raw JSON action log for archival or external processing

The full journey book appears in your Discord channel. No file extraction needed.

---

## Deduplication Engine

Raw gameplay is noise. The deduplication system has two mechanisms:

**Similarity window** — a configurable time window (in seconds) where similar action types are checked for repetition. "Traveled north" for the 40th consecutive tick doesn't get logged 40 times.

**Aggregate similar** — combines repetitive entries into a single counted entry: `"3× traveled 100 blocks north through forest"` instead of three separate movement entries. The AI gets count context without reading 40 identical lines.

Boss kills, dimension changes, and deaths are explicitly exempt from both mechanisms — they always appear in full.

---

## The In-Game Book — JourneyBookGUI

Configurable book cover style, border decoration, X/Y position on screen. Displays the current story as paginated readable text without leaving the game. `clear-actions-on-open` can reset the actions buffer when you open the book so you're always reading the freshest output, not a stale snapshot.

---

## ElytraSwap — The Module That Keeps You Flying Long Enough to Record Anything

Journey Recorder pairs naturally with ElytraSwap, which is one of the most underrated modules in the utility category. Here's what it actually does:

### Durability Warning and Auto-Replace

Monitors equipped elytra durability. At a configurable threshold, it warns you. At a second, lower threshold, if `auto-replace` is enabled, it **swaps in a fresh elytra from your inventory without interrupting flight**. You never notice. The broken elytra goes to inventory and a new one appears on your back.

### Elytra Fixer — Repairs Themselves

When you have Bottles o' Enchanting in your inventory, the **Elytra Fixer** sub-group watches all elytras that fall below a configurable durability floor and throws bottles at them automatically to repair them.

When the bottles run out:
- `auto-find-shulkers` — scans within a configurable range for shulker boxes and opens them to extract more bottles
- `inventory-shulker-mode` — opens shulker boxes from your inventory to get more bottles

Your supply of elytra is self-sustaining as long as you hold shulkers stocked with experience bottles.

### Mid-Air Repair Without Landing

This is the one that does it. `enable-mid-air-fix` allows repairing elytras **while flying**, without ever touching the ground:

**Platform mode** — places a temporary block above or below you, lands on it, runs the repair sequence, then `auto-break-platform` removes the block. You were never on the ground.

**Bottle-throw mode** — throws Bottles o' Enchanting upward at a configurable angle so they arc overhead and XP orbs fall on you mid-flight. Configure the throw angle (`throw-angle`), how many to throw before looking down to collect (`bottles-before-collect`), and how long to look down collecting orbs (`collect-duration` in ticks).

`auto-trigger-mid-air-fix` fires automatically when the number of broken elytras in your inventory hits a threshold. SafeWalk toggle during platform fixing prevents falling off your own platform.

With ElytraSwap running alongside Journey Recorder and AFKVanillaFly, your elytra supply manages itself for the entire session.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
