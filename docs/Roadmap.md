# FOOT — Roadmap

What exists, what's next, and what waits.

---

## What Is Already Built

**The chain.** Deterministic genesis. Reward formula. Floor price formula. Fork resolution by cumulative GB and tip hash. Fee pool distribution every 100 blocks.

**The network.** Nodes connect over a public relay. Any node behind carrier-grade NAT can participate. No port forwarding. No public IP. No VPS.

**Snapshot and prune.** Every 100,000 blocks, nodes freeze their state into a snapshot and delete all blocks below the tip. New nodes sync from a snapshot in seconds instead of downloading the full chain.

**FootNode (Android).** Working miner. Produces FOOT. Auto-resumes mining on restart. Full command interface.

**FOOT Wallet (Android).** Working wallet. Creates and imports wallets. Shows balance in real time. Sends and receives FOOT. Displays mining rewards as a running total. Caches to disk for offline viewing.

**FootNode (Desktop).** Same as the Android node, packaged for Windows, Mac, and Linux. Runs headless with a command interface.

---

## Phase 1 — The Game

**What:** A football manager game, in the tradition of Football Manager. Async multiplayer. Real FOOT economy on the chain.

**Core loop:**

1. Manager signs a player. Contract cost is paid in FOOT, on-chain.
2. Tactics set locally. Match simulates on the manager's device.
3. Both managers sign the result. Chain records it.
4. League table updates from signed results.
5. Season ends. Prize money pays out in FOOT.
6. Manager spends on better players, bigger stadiums, higher wages.

**Where FOOT flows:**

- Player transfers
- Player contracts (wages in escrow)
- Stadium rent
- Match fees
- League prizes
- Scout fees
- Agent commissions

**Technology:** Godot 4 .NET. Pre-made rigged 3D player assets. Mobile renderer.

**Platform:** PC first. Mobile later.

**Distribution:** itch.io and direct download initially.

**Status:** Design phase. Not started.

**Time estimate:** 18 to 24 months from first line of code.

---

## Phase 2 — Real Player Certification

**What:** Footballers connect their real attributes to digital twins in the game.

**How it works:**

- A footballer submits their attributes.
- The submission is certified by a coach, academy, or verified training session.
- The digital twin enters the player pool as a signed, real-player entity.
- Managers can contract the twin like any other player.
- The footballer earns FOOT when their twin is signed.

**Why it matters:** Every footballer's skill becomes a tradeable digital asset. Managers get real people. Footballers get a second income stream. The player pool expands beyond what the game generates.

**Requirements:**

- A certification mechanism for coach and academy signatures
- An attestation format the game can read
- A contract type for real-player twins
- Legal review on likeness and image rights

**Status:** Not started. Depends on Phase 1 being live with real users.

**Time estimate:** 12 months after Phase 1 launches.

---

## Phase 3 — The Wearable

**What:** A physical device a footballer wears during training that reads their physical activity and updates their digital twin automatically.

**What it measures:**

- Speed, distance, sprints
- Touches and ball control
- Heart rate and recovery
- Session volume and intensity

**What it does not measure:**

- "Shooting ability" or "passing accuracy" as single attributes
- Decision-making
- Football intelligence

The output is raw physical data. Attributes are derived by the game's attribute engine.

**Why it matters:**

- Removes the trust problem from Phase 2
- Continuous, automatic updates to digital twins
- Creates a hardware product tied to the FOOT economy
- Footballers who train see their digital value rise in real time

**Requirements:**

- Hardware design and certification
- Manufacturing partner
- Firmware development and update pipeline
- Support and warranty infrastructure
- Capital for production runs

**Estimated cost:** $50,000 to $500,000 to first shipped unit.

**Status:** Idea. Not feasible as a solo developer.

**Time estimate:** 3 to 4 years after Phase 2 launches.

---

## Phase 4 — The Licensing Market

**What:** A full market where footballers list their digital twins, managers bid, and contracts settle on-chain.

**How it works:**

- A footballer's digital twin is a licensable asset.
- Managers browse the market and bid.
- Contracts specify duration, wages, usage rights, revenue split.
- Everything settles in FOOT.
- The footballer earns a share of everything their twin produces — match appearances, goals, trophies, transfers.

**Why it matters:** Football's physical market connects to its digital market. Every manager in the game becomes a potential buyer. The footballer's skill becomes liquid.

**Requirements:**

- Legal framework for likeness licensing
- Dispute resolution for contract violations
- Reputation system for managers and footballers
- Integration with the real football industry

**Status:** Vision only.

**Time estimate:** 5+ years.

---

## The Compounding Loop

Each phase makes the next phase possible.

1. Game grows → more FOOT demand
2. FOOT demand grows → floor rises → mining becomes more valuable
3. More mining → more FOOT supply → the game has liquidity
4. Real players join → the game gets better → more managers
5. Wearables appear → more real players → tighter loop
6. Licensing market → the football industry connects → FOOT becomes a real commodity

Each phase is optional. The loop works without them. Each phase makes it faster and wider.

---

## The Single Sentence

**The game is not the product. FOOT is the product. The game is what FOOT is for. Every future layer serves that same purpose.**
