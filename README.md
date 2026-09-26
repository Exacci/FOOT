# FOOT

A commodity produced from data.

---

## Download

**Latest release:** [See the Releases page](../../releases/latest)

| File | Platform | What it is |
|---|---|---|
| `footnode.apk` | Android | The miner that produces FOOT |
| `footwallet.apk` | Android | The wallet that holds FOOT |
| `footnode.jar` | Windows / Mac / Linux | The desktop miner |

---

## What FOOT is

FOOT is a digital commodity. It is produced by burning gigabytes of data. Every GB consumed by the network mints a small amount of FOOT at a rate that decays forever. The floor price rises continuously as more data is burned. It cannot fall.

FOOT is not a cryptocurrency. It is not a token. It is not a security. It is a commodity, produced by work, held in a wallet, transferred between addresses.

The software in this repository is what produces, holds, and moves it.

---

## The three pieces of software

| Software | What it does |
|---|---|
| **FootNode** | Produces FOOT by burning data |
| **FOOT Wallet** | Holds FOOT, sends and receives it |
| **FootNode (Desktop)** | The same miner, for Windows / Mac / Linux |

FootNode is not the commodity. FOOT is the commodity. FootNode is the machine that produces it.

---

## How FOOT is produced

Every FootNode burns 0.00001 GB per second. One block is produced every ten seconds. Each block mints FOOT at the current reward rate.

The reward decays forever:

    reward = 10 / (1 + 0.000001 × totalGB)

The floor price is the inverse of the reward:

    floor = 1 / reward

At genesis, the reward is 6.228 FOOT/GB and the floor is $0.1606. As GB burns, the reward falls and the floor rises.

`totalGB` is the cumulative gigabytes burned by the entire network since genesis. The full model, including why the floor cannot fall and what each variable means, is in the [whitepaper](docs/WHITEPAPER.md).

---

## How node count affects the price

A node is any device running FootNode. Every node burns the same amount of data. More nodes means more burn, which means the floor price rises faster.

Here's the difference node count makes, at one year:

| Nodes | GB burned per day | Floor price after 1 year |
|---|---|---|
| 100 | 86 | $0.16 |
| 1,000 | 864 | $0.19 |
| 10,000 | 8,640 | $0.48 |
| 100,000 | 86,400 | $3.31 |
| 1,000,000 | 864,000 | $31.30 |

The formula never changes. The rules never change. The only thing that changes is how many people are running a node.

**More nodes, faster rise.**

---

## Running a node

### Android — the simple setup

Install FootNode and FOOT Wallet on the same phone.

1. Download `footnode.apk` and `footwallet.apk` from the latest release
2. Install both
3. Open **FOOT Wallet** → Create New Wallet → write down the 12 words
4. Copy the wallet address
5. Open **FootNode** → type: `start MFT-your-address`

Production begins. The wallet shows your FOOT balance in real time.

The wallet reads the chain from the node on the same phone. No configuration needed.

### Desktop

1. Install Java 11 or newer
2. Download `footnode.jar` from the latest release
3. Run it: `java -jar footnode.jar`
4. Type `help` for commands

---

## Running the node and wallet on different phones

This is a common setup. You keep the mining phone at home, plugged in and running 24/7. You carry the wallet phone with you.

Both phones work together as long as they're on the same WiFi.

### How it works

The wallet talks to the node over your home WiFi. The node doesn't need to be on the same phone as the wallet. It just needs to be reachable on the same local network.

### Setup

**Phone A — the mining phone (stays at home):**

1. Install **FootNode**
2. Open it. Type: `showip`
3. Write down the local IP address it shows. Example: `192.168.1.42`
4. Type: `start MFT-your-address`
5. Plug the phone in. Leave it running.

**Phone B — the wallet phone (goes with you):**

1. Install **FOOT Wallet**
2. Open it → **Create New Wallet** (or **Import Wallet** to use the same wallet as Phone A)
3. Open **Settings**
4. Change **Host** from `127.0.0.1` to the IP you wrote down: `192.168.1.42`
5. Change **Port** to `8334` if it isn't already
6. Tap **Save**
7. Go back to the Home screen

Phone B's wallet now reads from Phone A's node. Balance updates in real time. You can send and receive FOOT from Phone B.

### The one rule

Both phones must be on the same WiFi. If Phone B leaves the local network and switches to mobile data, it can't reach Phone A anymore. The wallet shows an "Offline" message until Phone B is back on the home WiFi.

### Two phones both mining to the same wallet

Phone B can also run FootNode if you want double the production.

1. Install **FootNode** on Phone B as well
2. Type: `start MFT-your-address` (same address as Phone A)

Both phones now mine to the same wallet. Balance grows twice as fast.

---

## Mining across different networks

You don't need the two phones to be on the same WiFi for mining to work.

- Phone A on one WiFi network, Phone B on a different WiFi network — both mine, both produce, both stay in sync.
- Phone A on WiFi, Phone B on mobile data — same.
- Two devices on two different continents — same.

**Each device connects out to the internet on its own. The internet connects them all together.** You never enter another device's IP address. You never set up a VPN. You never change router settings.

The one exception: if you want Wallet on Phone B to read from Node on Phone A, they must be on the same WiFi. That's the wallet-to-node link. Mining itself works anywhere.

---

## What FOOT is not

- Not a cryptocurrency
- Not a token
- Not a security
- Not listed on any exchange, foot is not Cryptocurrency, foot is different

FOOT is a commodity. It is produced, held, and transferred. There is no market price. The only price is the floor, which is a formula.

---

## Support

X: https://x.com/EXACCI

**I will never DM you. I will never ask for your seed phrase or private key. I will never ask for funds. Anyone claiming to be me and doing those things is a scammer.**

---

## Source code

This repository distributes compiled software only. The source is not published.
