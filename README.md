# FootNode

A commodity produced from data.

---

## Download

**Latest release:** [See the Releases page](../../releases/latest)

| File | Platform | What it is |
|---|---|---|
| `footnode.apk` | Android | The miner node |
| `footwallet.apk` | Android | The wallet |
| `footnode.jar` | Windows / Mac / Linux | The desktop node |

---

## What this is

FOOT is a digital commodity. It is produced by burning gigabytes of data. Every GB consumed by the network mints a small amount of FOOT at a rate that decays forever. The floor price rises continuously as more data is burned. It cannot fall.

The software in this repository is what runs the network.

---

## How it works

Every node burns 0.00001 GB per second. One block is produced every ten seconds. Each block mints FOOT at the current reward rate.

The reward decays forever:

    reward = 10 / (1 + 0.000001 × totalGB)

The floor price is the inverse of the reward:

    floor = 1 / reward

At genesis, the reward is 6.228 FOOT/GB and the floor is $0.1606. As GB burns, the reward falls and the floor rises.

---

## Running a node

### Android

1. Download `footnode.apk` and `footwallet.apk` from the latest release
2. Install both
3. Open **FOOT Wallet** → Create New Wallet → write down the 12 words
4. Copy the wallet address
5. Open **FootNode** → type: `start MFT-your-address`

Mining begins. The wallet shows your balance in real time.

### Desktop

1. Install Java 11 or newer
2. Download `footnode.jar` from the latest release
3. Run it: `java -jar footnode.jar`
4. Type `help` for commands

---

## What FOOT is not

- Not a cryptocurrency
- Not a token
- Not a security
- Not listed on any exchange and not meant for that. foot is different

FOOT is a commodity. It is produced, held, and transferred. There is no market price. The only price is the floor, which is a formula.

---

## Documentation

- **[Whitepaper](docs/WHITEPAPER.md)** — the full technical description
- **[User Guide](docs/USER-GUIDE.md)** — how to install and run a node
- **[Game & SDK Design](docs/GAME-SDK.md)** — how the game and SDK work
- **[Roadmap](docs/ROADMAP.md)** — what's next

---

## Support

X: [@yourhandle](https://x.com/yourhandle)

**I will never DM you. I will never ask for your seed phrase or private key. I will never ask for funds. Anyone claiming to be me and doing those things is a scammer.**

---

## Source code

This repository distributes compiled software only. The source is not published.
