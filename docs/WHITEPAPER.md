# FOOT

### A commodity produced from data

**Pseudonymous**

**Version 1.0 — September 2026**

---

## Abstract

FOOT is a digital commodity produced from data consumption. Every gigabyte burned by a node mints FOOT at a rate that decays forever. The floor price of FOOT is the inverse of the reward and therefore rises continuously over time. The network runs on ordinary phone hardware, behind carrier-grade NAT, without port forwarding, without a VPS, and without any infrastructure operated by the author. A game development SDK allows third-party games to accept FOOT as currency. This paper describes the mechanism, the transport, the consensus rules, and the SDK.

---

## 1. Motivation

Three problems exist at the intersection of digital economies and the people who live outside them.

**Crypto assets are volatile.** A digital currency that swings 80% in a week cannot serve as a unit of account for anything. Games that depend on such currencies collapse when the price crashes. Users are punished for participating.

**Mining networks require infrastructure.** Bitcoin mining requires specialized hardware and cheap electricity. Running a full node requires a public IP. Neither is available to a person with a mid-range Android phone and a mobile data plan.

**Data consumption produces nothing.** Every person on earth consumes gigabytes daily. That consumption leaves no trace and creates no value for the person who did the consuming.

FOOT addresses all three. It is a commodity with a mathematically rising floor, not a traded asset. It runs on the hardware people already own. It converts data consumption into a measurable product. A game SDK lets any developer plug it into their own project without understanding the chain.

---

## 2. The Commodity Model

FOOT is minted when a node burns a gigabyte. The reward per gigabyte is:

    reward = 10 / (1 + 0.000001 × totalGB)

Where `totalGB` is the cumulative gigabytes burned by the entire network since genesis. At genesis, `totalGB = 605,600`, giving an initial reward of 6.228 FOOT per gigabyte. The reward decays forever and is floored at 0.001 FOOT per gigabyte.

The floor price of FOOT is:

    floor = 1 / reward

At genesis, the floor price is $0.1606 USDT equivalent. Because the reward decreases as GB is burned, the floor rises as the network operates. The floor is a formula, not a market quote. It cannot be manipulated downward by selling pressure.

This design has three consequences:

- The supply of FOOT grows without bound but at a decaying rate.
- The floor price rises continuously, with no mechanism to reverse.
- The cost of producing a FOOT rises over time, because the reward per GB falls.

These are the properties of a commodity with declining yield. Gold behaves this way. Oil behaves this way. FOOT is designed to behave this way.

The practical effect of the formula is that the floor price rises faster when more nodes are burning data. A table showing the floor price after one year at 100, 1,000, 10,000, 100,000, and 1,000,000 nodes is in the User Guide.

---

## 3. Genesis

The chain begins with a single block containing one transaction: a mint of 4,736,000 FOOT to an address called the vault. This is equivalent to having burned 605,600 GB at the moment of launch. The vault is a fixed allocation, verifiable on-chain, held by the author for distribution to early participants.

Genesis is deterministic. Every node that installs the software produces the same genesis block with the same hash. There is no coordination required and no trust in the author required for genesis to be correct.

---

## 4. The Network

FOOT nodes communicate over MQTT through a public broker. This is a deliberate design choice with a specific purpose.

**The problem.** Two phones on mobile data both sit behind carrier-grade NAT. Neither can accept an incoming connection. Standard peer-to-peer protocols require at least one side to be dialable. On mobile networks, neither side is.

**The solution.** Every node dials outbound to a public MQTT broker. The broker is reachable from any network. Nodes publish blocks and transactions to a shared topic. Every node subscribed to that topic receives every message. No node needs a public IP.

The trade-off is explicit: transport is centralized through the broker, while chain state remains fully distributed. Each node holds the full chain. Each node validates every block independently. The broker cannot alter a block, forge a transaction, or change a balance. It only moves bytes between open connections.

**Topics:**

- `footnode-foot-v1/blocks` — blocks and transactions
- `footnode-foot-v1/snapshot-requests` — chain snapshot requests

**Message types:**

- `HELLO <peerId>` — announces a node
- `TIP <peerId> <height> <gb> <hash>` — announces the current chain tip
- `BLOCK <json>` — a full block
- `TX <json>` — a signed transaction
- `SNAPSHOTREQ` / `SNAPSHOT <json>` — chain state transfer

---

## 5. Mining and Consensus

Mining rate is fixed per node. Every node burns 0.00001 GB per second while mining, producing a block every ten seconds. There is no proof-of-work, no difficulty adjustment, and no competition for block production. Every node on the network mines at the same rate.

Because mining is not competitive, blocks are produced frequently and forks are common. When two nodes produce a block at the same height within the same moment, the network has two candidate chains. Resolution follows a deterministic rule:

1. The chain with greater cumulative GB wins.
2. If cumulative GB is equal, the chain whose tip block hash is numerically lower wins.

Every node applies this rule identically. Every node reaches the same conclusion from the same pair of chains. No voting, no coordination, no trust.

Deep forks — cases where two nodes have mined in full isolation for hundreds of blocks — are resolved by a snapshot request. The node with the heavier chain sends its full state to the node with the lighter chain, which replaces its chain and continues from the new tip.

---

## 6. Snapshot and Prune

A chain that grows forever becomes unusable on phone hardware. FOOT prunes.

Every 100,000 blocks, a node computes a snapshot: the current balance of every address, all nonces, the total GB burned, the mining supply, and the tip block itself. The snapshot is written to disk. All blocks below the tip are deleted. Memory keeps only the tip.

On startup, a node loads the snapshot if present. It does not replay from genesis. Boot time stays constant regardless of chain age.

New nodes that are more than 500 blocks behind the network request a snapshot from any peer. The peer responds with its current state. The new node verifies the snapshot's tip block hash, applies the state, and continues from that point. Chain sync that would have taken hours takes seconds.

---

## 7. The SDK for Game Builders

FOOT is not useful without a consumer product. Rather than force every game to be built by the author, FOOT provides an SDK that any game developer can integrate into their own project.

**What the SDK is.** A small library written in C# for Godot 4 .NET projects. It handles wallet generation, transaction signing, balance queries, and broadcasting. The game developer never touches the chain directly.

**What it looks like in use.**

    var wallet = Foot.Wallet.FromSeed("apple tiger river ...");
    var client = new Foot.Client(connectionString);

    double balance = client.GetBalance(wallet.Address);
    client.Send(wallet, recipientAddress, 10.0);

Three lines to receive FOOT. Three lines to send FOOT. The SDK handles all cryptography, nonce management, signature construction, and network communication.

**What it does NOT do.** The SDK does not include the node. It talks to one over a connection the game developer provides.

**Why this matters.** A game that wants to use FOOT does not need to understand the chain's consensus rules, implement secp256r1 cryptography, manage nonces, handle MQTT, or run a node itself. It just includes the SDK.

**Language support plan.**

- **C#** (Godot 4 .NET, Unity) — first version
- **JavaScript** (web games, HTML5) — second version
- **Python** (pygame, small indie games) — third version
- **GDScript wrapper** — for Godot developers who prefer GDScript

**The economic effect.** Every game that integrates the SDK becomes a new source of FOOT demand. Their players earn FOOT, hold FOOT, and spend FOOT inside the game. Every integration deepens the economy. FOOT becomes the settlement layer for a category, not one game.

---

## 8. Utility — The Football Manager Game

The first consumer product is a football manager game, in the tradition of Football Manager. Async multiplayer. One to thirty-two human managers per league.

**The loop:**

1. A manager signs a player. Contract costs FOOT, paid from wallet to wallet, on-chain.
2. Tactics are set locally. The match simulates on the manager's device.
3. Both managers sign the result. It writes to the chain.
4. The league table updates from signed results.
5. The season ends. Prize money pays out in FOOT from the league treasury.
6. The manager spends it on better players, bigger stadiums, higher wages.

**Where FOOT flows:**

- **Player transfers** — the only way to acquire a player
- **Player contracts** — wages locked in escrow, released per match
- **Stadium rent** — recurring per-home-match payment from manager to stadium owner
- **Match fees** — small fee split between stadium owner and league treasury

Four required paths. There is no way to play the game without FOOT.

**No central server.** Matches simulate on player devices. The chain records economic events only. The game does not run on a server, and no operator can shut it down.

---

## 9. The Long-Term Roadmap

**Phase 1 — The Game.** Football manager with async multiplayer and a real FOOT economy. Fictional players.

**Phase 2 — Real Player Certification.** Footballers connect their real attributes to digital twins in the game. A coach or academy certifies the attributes. Managers contract the twin like any other player. The footballer earns FOOT when their twin is signed.

**Phase 3 — The Wearable.** A physical device worn during training that measures physical activity and updates the digital twin automatically. Removes the trust problem from Phase 2. Requires hardware design and manufacturing.

**Phase 4 — The Licensing Market.** Footballers list their digital twins. Managers bid. Contracts settle on-chain. Football's physical market connects to its digital market.

**The compounding loop:** the game grows demand for FOOT, which raises the floor, which makes mining more valuable, which brings more nodes, which makes the game's economy more liquid, which brings more managers. Each phase accelerates the loop.

---

## 10. Conclusion

FOOT is a commodity produced by data consumption, with a mathematically rising floor, on hardware that ordinary people own. It has no premine beyond the vault, no governance, no foundation, and no investor allocation. It runs today.

The next step is not a token sale. It is a game.

---

## FAQ — Twenty Technical Questions

**1. What is FOOT?**
A commodity produced by data consumption. Every gigabyte burned by a node produces FOOT at a decaying rate. The floor price rises as the reward decays.

**2. Is FOOT a cryptocurrency?**
No. FOOT is a commodity. It is not listed on an exchange. It has no market price. It is produced, held, and transferred, like gold or oil.

**3. How do I get FOOT?**
By running a node. Install FootNode, point it at your wallet address, and mine. There is no way to purchase FOOT. Mining is the only distribution mechanism at launch.

**4. What is the floor price?**
`1 / reward`. At genesis, $0.1606 USDT. The floor rises as the total GB burned increases. It cannot fall.

**5. Why does the floor rise?**
Because the reward falls. Every GB burned reduces the reward per GB for all future mining. As the reward falls, its inverse — the floor — rises. This is arithmetic, not policy.

**6. What is the vault?**
4,736,000 FOOT minted at genesis to a single address, equivalent to having burned 605,600 GB at launch. The vault is held by the author for distribution to early participants. Its balance is public and verifiable on-chain.

**7. What stops someone from mining a fake chain?**
Nothing. But the fake chain has less cumulative GB than the real one, because the real network has been mining continuously. When the fake chain is published, the network compares cumulative GB and rejects it.

**8. What is the consensus mechanism?**
There is no classical consensus. Mining rate is fixed per node. Fork resolution is by cumulative GB, then by lower block hash. Every node reaches the same conclusion from the same chain.

**9. Why MQTT instead of libp2p?**
Because phones on carrier-grade NAT cannot accept incoming connections. MQTT is outbound-only, works through CGNAT, and runs on a free public broker. Libp2p requires a public relay or a full rewrite of the P2P layer.

**10. What happens if the broker goes down?**
The chain survives on every node. The network pauses. No new blocks are produced until a broker is reachable. Migration to a new broker is a one-line change in the node software.

**11. Can the broker steal my FOOT?**
No. The broker never holds keys and never signs transactions. It moves bytes between open connections. Every block is validated independently by every node.

**12. Can I lose my FOOT?**
Yes, if you lose your twelve-word seed. There is no recovery. The seed is the wallet. Back it up offline.

**13. Can I sell my FOOT?**
Off-chain, at your own risk, to whoever wants to buy it. The network does not provide a market. There is no exchange listing and none is planned.

**14. Can I buy FOOT?**
Not on-chain. You can receive FOOT from someone who mined it. You can mine it yourself. There is no purchase mechanism at launch.

**15. What is the initial supply?**
4,736,000 FOOT at genesis, all held by the vault. Additional FOOT is minted as the network mines, at a rate that decays over time.

**16. How fast is FOOT produced?**
One block every ten seconds per node. Each block burns 0.0001 GB. The reward per block at genesis is approximately 0.0006228 FOOT.

**17. Can one person run many nodes?**
Yes. That is by design. FOOT does not attempt to make mining scarce, only accessible. A person with more hardware earns more.

**18. How is this different from Bitcoin?**
Bitcoin mining requires specialized hardware. FOOT runs on phones. Bitcoin's nodes require public IPs. FOOT's work through CGNAT. Bitcoin has a fixed supply cap. FOOT does not. The two systems solve different problems.

**19. How is this different from Pi Network?**
Pi is a centralized ledger with a mobile front end. Every Pi "node" reports to a central server. FOOT nodes hold the full chain and validate every block independently. There is no central server.

**20. Who are you?**
Pseudonymous. The system is open-source at the level of its software and verifiable at the level of its chain. Judge it on its merits. If there is ever a reason to reveal, I will.

---

## Appendix — How the SDK Positions FOOT

Every game that integrates the SDK becomes a FOOT consumer.

**The SDK is small.** A C# library that hides all chain complexity. Game developers add it and use three lines of code. They never touch crypto.

**The SDK is not a node.** It talks to a node over a connection the game developer configures.

**The SDK turns any game into a FOOT economy.** A racing game, a strategy game, a farming game. Any game with an economy can use FOOT as its currency. FOOT becomes the settlement layer for a category, not just one game.

**The economic effect.** Every SDK integration increases FOOT demand. Every game becomes a new source of miners-turned-buyers, and buyers-turned-miners. The more games use FOOT, the more important FOOT becomes — not because more people want to hold it, but because more games require it to function.

That is what makes FOOT important. Not the price. Not the marketing. The fact that a growing number of games cannot run without it.￼Enter
