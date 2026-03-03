# 📖 Journey Recorder

> *Your adventures, written by AI. Every session becomes a story worth reading.*

---

Most of what happens in Minecraft disappears when you log out. Coordinates you forgot to note. The cave system you cleared last Tuesday. The moment you stumbled into a stash you're now ninety percent sure was near a mesa biome. Gone.

Journey Recorder fixes that — and goes further, turning raw gameplay data into readable narrative using AI.

---

## What It Records

Journey Recorder tracks your session in real time:

- **Movement** — not just "traveled 200 blocks" but *which direction, from where, through what biome, at what height, how fast*
- **Mining and gathering** — what you found, how deep, how many total so far this session
- **Combat** — who you fought, where, whether it was PvP or mobs, how many you've killed overall
- **Dimension transitions** — every portal, every End gateway, every Nether crossing
- **Deaths and respawns**
- **Notable discoveries** — rare blocks, boss encounters, anything that breaks the pattern

---

## How Stories Are Generated

When you choose to generate, Journey Recorder sends your annotated session data to a HuggingFace AI model. It returns a narrative — as long or short as you configure — that reads like an actual account of what happened.

The richer the input, the better the story. Journey Recorder is specifically designed to give the AI useful context:

- Biomes are formatted as readable names, not internal IDs
- Distances include your starting point so the AI understands scale
- Combat events include kill counts so the AI knows whether this was one encounter or a running battle
- Height context tells the AI you were deep underground, not just "at Y=-52"

The AI gets enough to write something worth reading. You get a story instead of a log.

---

## Smart Deduplication

Raw gameplay produces a lot of noise. Walking 3,000 blocks generates hundreds of movement ticks. Journey Recorder consolidates them:

- Multiple movement entries within a time window are merged into one directional summary
- Repeated similar actions are aggregated with a count rather than repeated verbatim
- Spam is filtered before it reaches the AI
- Boss kills, dimension changes, and deaths are always preserved regardless of deduplication settings

---

## Output Formats

Stories are saved to text files in your Minecraft folder. Configure:

- **Append mode** — each session adds a new chapter to the same file
- **Overwrite mode** — each session starts fresh
- **Raw data backup** — the full action log is always saved in JSON for later reuse or re-generation

---

## Setup

You need a HuggingFace account (free tier works) and an API token. Set the token once in the module settings or via environment variable, point it at a model of your choice, and it runs in the background automatically.

---

*Part of Skylandia's Automation category.*  
*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
