# 📖 Journey Recorder

> *Your adventures, written by AI. Every session becomes a story worth reading.*

Most of what happens in Minecraft disappears when you log out. Journey Recorder fixes that — and goes further, turning raw gameplay data into readable narrative using AI.

---

## What It Records

Journey Recorder tracks your session in real time across six data layer types:

- **Movement** — direction, biome, height, origin distance, speed profile
- **Mining and gathering** — block type, depth, session cumulative count, rarity context
- **Combat** — entity type, location, kill count, PvP vs mob flag
- **Dimension transitions** — every portal, End gateway, Nether crossing with entry/exit coordinates
- **Deaths and respawns** with cause and location
- **Notable discoveries** — rare blocks, boss encounters, structure entries

---

## How Stories Are Generated

When you trigger generation, Journey Recorder sends annotated session data to a HuggingFace AI model configured in your settings. The annotations include biome readable names (not internal IDs), kill counts for combat context, height classification for underground vs. surface distinction, and distance-from-origin for narrative scale.

The AI receives enough context to write something worth reading rather than a timestamped log.

---

## Smart Deduplication

Raw gameplay produces noise. Journey Recorder consolidates it:

- Movement entries within a time window are merged into directional summaries
- Repeated similar actions aggregate with a count
- Boss kills, dimension changes, and deaths bypass deduplication and are always preserved

---

## Output and Storage

- Stories save to text files in your Minecraft folder
- Append mode (chapters accumulate) or overwrite mode (per-session fresh start)
- Raw action log always saved in JSON for re-generation or external use

**JourneyBookGUI** — a separate in-game GUI module — lets you browse and read saved journey files without leaving the game. Presents stories as readable books with pagination.

**AIStoryGenerator** is the backend component that manages the HuggingFace API connection, model selection, prompt templating, and response parsing independently from the recorder.

---

## Setup

You need a HuggingFace account (free tier works) and an API token. Set the token once in module settings or via environment variable. Points at any compatible model.

---

## Other Utility Modules

Journey Recorder lives in Skylandia’s Utility category alongside an unusually deep set of companion modules:

### GrimEfly
Chestplate-based elytra flight that uses the bounce exploit to stay airborne without equipping an elytra — meaning **your elytra never takes durability**. Settings include bounce auto-mode with configurable pitch lock (default 90°) and yaw lock, a custom yaw mode for non-45° angles, and an **Obstacle Passer** subsystem that handles terrain interruptions mid-flight. Integrates with Baritone for ground-rerouting when ceilings are too low.

### ElytraSwap
Intelligent elytra durability manager. Monitors equipped elytra durability and warns at a configurable threshold. **Auto-replace** swaps in a fresh elytra from your inventory when durability drops below a second threshold, without interrupting flight. **Elytra Fixer** automatically repairs all damaged elytras in your inventory using Bottles o’ Enchanting when they cross a durability floor. Also handles held-elytra swapping for the GrimEfly workflow.

### OllamaBotModule
In-game AI chat assistant via a local [Ollama](https://ollama.com/) instance. Listens for a configurable trigger prefix (default `!ask`) in chat and routes the message to your local LLM via the Ollama API at `localhost:11434`. Maintains a 10-message rolling context window so multi-turn conversations work naturally. Configurable system prompt for personality, respond-to-all mode, whitelist of allowed users, and a model refresh button that queries Ollama for available models. Runs on a two-thread executor so the game never blocks waiting for a response.

### SecureChatModule
Client-side encrypted messaging layer over the standard Minecraft chat channel. Encrypts outgoing messages and decrypts incoming ones for other Skylandia users on the same key. Also hosts custom chat filter rules. Used by ShulkerTransportModule for inter-account coordination.

### GrimDuraFirework
Conserves elytra durability under Grim anti-cheat by intelligently timing firework use to avoid the server-side durability deduction window. Necessary for long-distance flight on Grim-protected servers.

### AutoLoginModule
Automates the login sequence on servers that require `/login <password>` or similar commands after connect. Configurable command and delay. Pair with the proxy settings for full automated reconnect.

### Numerology
Coordinate analysis and mathematical utility module for seed-based location calculations and Randar-compatible coordinate math.

> The Utility category also contains ActivatedSpawnerDetector, BungeeSpoofer, EnchantedAnvil, Firework, InfiniteTools, Pitch40Util, SignHistorian, TrackerModule, BaritonePathing, ServerScannerModule, and more.

---

*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
