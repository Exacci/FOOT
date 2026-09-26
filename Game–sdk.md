# FOOT — Game and SDK Design

How the football manager game and the SDK for game builders work.

---

## Part 1 — Why FOOT Exists for Gamers and Game Developers

### The problem with crypto games

Every crypto game in the last five years has followed the same pattern:

1. Launch a token
2. Give tokens to early players
3. Watch the price rise
4. Watch the price collapse when the game can't absorb new supply
5. Game dies

The collapse always comes from the same root cause: the token has no natural consumer. Players earn it and immediately sell it. Nothing in the game requires holding it. So nobody holds it.

### What's broken for game developers

A developer who wants a real economy in their game has three bad options:

**Option A — Build your own chain.** Months of work, expert cryptography, ongoing security risk. Nobody does this correctly.

**Option B — Use an existing crypto token.** Volatile, speculative, and legally ambiguous. Players lose money when the price moves. Regulators notice.

**Option C — Keep it in-game only.** Closed economy, no real value, no cross-game value, no external liquidity. The currency is a number in a database you control.

None of these are good. Most developers choose C and accept the limits.

### What FOOT offers both sides

**For gamers:**

- A currency with a mathematically rising floor. It cannot be worth less tomorrow than the formula says today.
- Guaranteed exit. If you want out, the game buys your FOOT back at the floor. Always available.
- No speculation needed. You don't have to believe in a price. The floor is arithmetic.
- Real ownership. FOOT lives on a chain, not in a game's database.
- No premine, no token sale. The only FOOT in existence was produced by running nodes.

**For game developers:**

- A real economy without building a chain. Drop the SDK into your Godot project. Three lines of code and your game accepts FOOT.
- No volatility risk to your players. The floor protects them.
- No legal ambiguity about the token. FOOT is a commodity, not a security.
- An SDK that hides all complexity. You never touch cryptography, nonces, or the network layer.
- Works on any network. Mobile carriers, WiFi, hotspots. No port forwarding. No server.

### The core thesis

A commodity only matters when a real economy requires it to function.

Gold was money because empires ran on it. Oil matters because industry runs on it. FOOT matters when a game cannot run without it.

The first game that requires FOOT is a football manager. It will not be the last.

---

## Part 2 — The Football Manager Game

### Genre

A football manager game in the tradition of Football Manager. Async multiplayer. One to thirty-two human managers per league. Match results and economic events recorded on the FOOT chain.

Not FIFA. Not Dream League Soccer. Football Manager.

### Why this genre

Football manager fits a decentralized network better than any other genre.

| Requirement | Football Manager | Real-time 3D football |
|---|---|---|
| Match timing | Async, no simultaneity required | Real-time, both players online |
| State exchange | Only inputs and outcomes | Continuous state streaming |
| Connectivity | Works through CGNAT | Requires direct connections or servers |
| Determinism | Pure math, both sides agree | Physics, both sides drift |
| Solo dev scope | Achievable in 2–3 years | Not achievable |
| Server need | None | Required |

Football manager was the only genre that could work without a server. That's why it was chosen.

### The match model

Two managers play a match asynchronously by default.

1. Manager A commits their tactics (hash) to the chain
2. Manager B commits their tactics (hash) to the chain
3. Both managers reveal their tactics (full data) to the chain
4. Both devices compute the match locally using the same seed
5. Both managers sign the result
6. The chain records the result when both signatures match
7. The league table updates on every node

Live simultaneous matches are possible as an option for cup finals and derbies. Both managers agree on a kickoff time, both open the app, both watch the same simulation on their own device with the same seed.

### What is on-chain

- Player ownership
- Contracts and escrow
- Stadium ownership
- Match results
- League standings (derived from signed results)

### What is off-chain

- Match simulation
- Tactics
- Player attributes
- UI, animations, commentary
- Scouting and training

### Where FOOT flows

Every economic action is a FOOT transaction.

| Action | Payer | Receiver |
|---|---|---|
| Player transfer | Buying manager | Selling manager |
| Wage payment | Manager's escrow | Player's wallet |
| Stadium rent | Visiting manager | Stadium owner |
| Match fee | Both managers | Stadium owner + league treasury |
| League prize | League treasury | Manager |
| Scout fee | Manager | Scout |
| Agent commission | Manager | Agent |

There is no way to play without FOOT. There is no in-game currency that substitutes.

### The economy is denominated in FOOT

Every price is set once and never changes.

| Tier | Transfer fee | Wage per match |
|---|---|---|
| Youth prospect | 5–25 FOOT | 0.05 FOOT |
| Squad player | 25–150 FOOT | 0.2 FOOT |
| First team | 150–800 FOOT | 1 FOOT |
| Star | 800–5,000 FOOT | 5 FOOT |
| Generational | 5,000–50,000 FOOT | 25 FOOT |

The dollar value of these prices rises with the floor. The football economics never change.

### Mandatory roles

Every player in the game must have a role. No role, no play. Roles:

- **Manager** — owns a team, plays matches
- **Scout** — finds players, sells information
- **Stadium owner** — rents pitches, collects fees
- **Agent** — negotiates contracts, takes commission
- **Academy owner** — develops youth, sells to managers
- **League operator** — runs a league, pays prize money

Roles turn speculators into participants. Participants don't panic sell. They play.

### The exchange

The game operates its own exchange.

- **Entry:** Players buy FOOT at the game's price (floor + margin)
- **Exit:** Players sell FOOT back at the floor price (always available)
- **P2P:** Exists outside the game. Not facilitated by the game.

The game earns the spread on every entry and exit. The spread is the exchange's revenue.

### Payment rails

- Deposits: USDT (TRC-20) to game-controlled wallets
- Withdrawals: USDT out, minus a small fee
- No fiat. No bank. No payment processor.

### Visual target

The visual target is Football Manager 26 style — clean 3D models on a pitch, broadcast camera, focus on simulation depth rather than graphical fidelity.

Not photorealistic. Not FIFA. The match engine is math, not physics. The look is clean and readable, not cinematic.

This is not a limitation — it's the correct design for the genre. FM has looked this way for decades because the game lives in the simulation, not the graphics.

### Platform

- **PC first** (Windows via Godot 4 .NET)
- **Mobile later** (Android via Godot 4 .NET)
- **Distribution:** itch.io and direct download initially. Steam later if policy allows.

### The embedded wallet

The game ships with a wallet embedded. Players never install a separate wallet app.

- Game generates a wallet on first launch
- Seed stored securely on the device
- Wallet signs transactions silently
- Player sees a balance in the UI, nothing else

The player never knows they're on a chain. They just play.

---

## Part 3 — The SDK for Game Developers

### Purpose

Any game developer should be able to integrate FOOT without understanding the chain.

The SDK handles:

- Wallet generation from a seed
- Transaction signing
- Nonce management
- Communication with a node
- Broadcasting signed transactions

The game developer calls a few methods. Everything else is hidden.

### Public API

Written in C# for Godot 4 .NET and Unity.

```csharp
var wallet = Foot.Wallet.FromSeed("apple tiger river ...");
var client = new Foot.Client(connectionString);

double balance = client.GetBalance(wallet.Address);
List<Tx> history = client.GetHistory(wallet.Address);
double floor = client.GetFloorPrice();

Foot.Transaction tx = Foot.Transaction.Transfer(wallet, recipientAddress, 10.0, nonce);
client.Broadcast(tx);
