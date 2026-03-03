# 📦 Shulker Transport System

> *Two accounts. Two dimensions. One automated logistics pipeline.*

---

Moving items between the Overworld and the End on an anarchy server is one of the most logistically demanding tasks in the game. It requires timing, precision, multi-account coordination, and no room for error — because the End is not a forgiving place to be holding someone else's gear.

The Shulker Transport System automates the entire process.

---

## The Problem It Solves

On large anarchy servers, high-value item storage and transfer between dimensions requires:

1. Two players in the right positions at the right time
2. Exact pearl stasis chamber timing
3. Confirmation before irreversible inventory transfers
4. A recovery path if anything goes wrong

Manual coordination fails. This system doesn't.

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

The system is built around the assumption that things go wrong:

- Every transfer requires **explicit confirmation** from the Transporter before execution
- Items on the **blacklist** cannot be transferred — protecting valuables from accidental movement
- If the stasis chamber state is invalid, the sequence **stops and holds** rather than proceeding
- Timeout thresholds on every coordinated step — if either account stops responding, the system halts safely
- Full **rollback logic** if a step fails partway through

---

## Communication

The two accounts coordinate over Skylandia's SecureChat channel — an encrypted in-game messaging layer.

---

*Part of Skylandia's Automation category.*  
*Access requires Lotus Clan membership. [→ Find out how to join](../../README.md#-getting-access)*
