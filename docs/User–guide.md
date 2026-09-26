# FootNode — User Guide

Everything you need to know to start mining FOOT.

---

## What is FOOT?

FOOT is a digital commodity — like gold, but made from data.

You run an app called **FootNode** on your phone or computer. It produces FOOT for you, slowly, every day. You keep it in an app called **FOOT Wallet**. That's it.

---

## What You Need

**On your phone:**

1. **FootNode** — produces FOOT
2. **FOOT Wallet** — holds FOOT

Both are free.

You also need:
- An Android phone
- Internet (WiFi or mobile data — both work)
- A charger (so the phone stays on while mining)

**On your computer (optional):**

You can also run FootNode on a Windows, Mac, or Linux computer. It mines the same way and produces FOOT to the same wallet. Many users run both a phone and a PC to double their production.

You also need:
- A computer running Windows, Mac, or Linux
- Java 11 or newer installed
- A copy of `footnode.jar`
- Internet connection

---

## The Simplest Setup: Both Apps on One Phone

This is the standard way. Most users do this.

Both apps on the same phone. They find each other automatically. Nothing to configure.

**How to start:**

1. Install **FootNode**
2. Install **FOOT Wallet**
3. Open FOOT Wallet → **Create New Wallet** → write down the 12 words → copy the address
4. Open FootNode → type `start MFT-your-address` → press Enter
5. That's it. Mining starts.

**Works on WiFi. Works on mobile data. No setup needed.**

---

## Running the PC Version

The PC version does the same thing as the phone version. It mines FOOT to whatever address you tell it to.

**Setup:**

1. Install Java 11 or newer. On Windows or Mac, download it from the official Java installer. On Linux, install it from your package manager.
2. Download `footnode.jar` from the latest release.
3. Put the file in any folder you want. A folder like `Documents/FootNode` is fine.
4. Open a terminal or command prompt in that folder.
5. Run this command:

    java -jar footnode.jar

You'll see a startup log like this:

    FootNode starting
      Data directory : ...
      P2P port       : ...
      API port       : ...

    Genesis: 4736000.0 FOOT at MFT-3cc271...

    FootNode running. Type 'help' for commands.

**Start mining:**

Type this command in the same window:

    start MFT-your-address

Replace `MFT-your-address` with the address from your FOOT Wallet. Press Enter.

The PC is now mining. It runs until you close the window or type `exit`.

**The same commands work:**

Every command that works on the phone works on the PC. `status`, `balance`, `peers`, `price`, `vault`, `send`, `fee`, `backup`, `restore`, `exit`. Same names, same behavior.

**Keeping the PC mining:**

As long as the terminal window stays open, the PC keeps mining. If you close the window, mining stops.

To keep it running in the background on Linux or Mac:

    nohup java -jar footnode.jar &

Logs go to `nohup.out` in the same folder. The process keeps running after you close the terminal.

On Windows, leave the command prompt window open and minimize it.

**Mining on both PC and phone:**

You can run FootNode on your phone and your PC at the same time. Both mine. Both produce FOOT. Both can mine to the same wallet.

1. Open FootNode on your phone → `start MFT-your-address`
2. Open FootNode on your PC → `start MFT-your-address`
3. Both are now mining to the same wallet

The wallet grows twice as fast. Each device contributes independently.

The two devices find each other over the internet automatically. You don't need to configure anything between them. They just connect and sync.

---

## How Much FOOT You'll Earn

At launch rates, one device mines about:

- **5 FOOT per day**
- **38 FOOT per week**
- **160 FOOT per month**

Two devices mining to the same wallet mine twice as fast. Three devices mine three times as fast.

The reward rate goes down over time. But the floor price goes up. So your FOOT becomes worth more as time goes on.

---

## Why More Nodes Make FOOT More Valuable

Every node burns data. Every GB burned raises the floor price.

The floor is the guaranteed minimum price of FOOT. It rises as more data is burned. It can't fall.

Here's how many nodes it takes to reach different floor prices, in one year:

| Nodes | Floor price after 1 year |
|---|---|
| 100 | $0.16 |
| 1,000 | $0.19 |
| 10,000 | $0.48 |
| 100,000 | $3.31 |
| 1,000,000 | $31.30 |

**Every node you add makes the floor rise a little faster.**

When you run FootNode, you're not just earning FOOT. You're helping the whole network's floor price rise. The more people running nodes, the more valuable every FOOT becomes for everyone.

This is different from most projects. In most networks, adding more miners means each miner earns less. In FOOT, adding more nodes means everyone's FOOT becomes worth more over time.

You earn slower, but each FOOT is worth more. Both effects come from the same formula.

---

## The Two-Phone Setup: Mine on One Phone, Wallet on Another

You can mine on one phone and check your balance on another, as long as they're on the same WiFi.

**Why you might want this:**

- Keep the mining phone at home. Plugged in, screen off, always mining.
- Carry the wallet phone with you. Check your balance anywhere, send FOOT, receive payments.

**Step-by-step setup:**

**Phone A — the mining phone (stays at home):**

1. Install **FootNode** on Phone A
2. Open it. Type: `showip`
3. Write down the address it shows
4. Type: `start MFT-your-address`
5. Leave Phone A plugged in at home. Mining is running.

**Phone B — the wallet phone (goes with you):**

1. Install **FOOT Wallet** on Phone B
2. Open it → **Create New Wallet** (or **Import Wallet**)
3. Open **Settings** in the wallet
4. Change **Host** to the address you wrote down from Phone A
5. Change **Port** if it isn't already set correctly
6. Tap **Save**
7. Go back to the wallet Home screen

**Now what happens:**

- Phone B's wallet reads the chain from Phone A's node over WiFi
- Phone B shows the balance in real time
- You can send and receive FOOT from Phone B
- Phone A keeps mining in the background

**The only rule:** Both phones must be on the same WiFi. If Phone B leaves the local network and switches to mobile data, it can't reach Phone A anymore. The wallet will show an "Offline" message until Phone B is back on the home WiFi.

**If you want Phone B to mine too:**

Phone B can also run FootNode and mine.

1. Install **FootNode** on Phone B as well
2. Type: `start MFT-your-address`
3. Both phones now mine to the same wallet

Now you have two phones mining. Wallet grows twice as fast.

---

## Mining on Many Devices

You can run FootNode on as many devices as you want — phones, computers, or both.

- 10 devices → 10 times the mining
- 100 devices → 100 times the mining

**Two ways to set it up:**

**Way 1 — Each device has its own wallet**

Every device creates its own wallet with its own address. Each device mines to its own wallet.

Use this if different people own different devices.

**Way 2 — All devices mine to one wallet**

Every device mines to the same address. All FOOT collects in one wallet.

Use this if one person owns all the devices.

**Both ways work. Choose based on who owns what.**

---

## How Devices Connect — Explained Simply

**Each device connects to the internet on its own.**

It doesn't matter if you have:

- One phone on WiFi
- Two phones on the same WiFi
- Two phones on different WiFi
- Phones on mobile data
- A phone on mobile data and a PC on WiFi
- Devices in different cities
- Devices in different countries

**Every device connects out to the internet. The internet connects them all together.**

You never have to:

- Enter another device's address
- Set up a VPN
- Change router settings
- Forward ports
- Pair devices

Just make sure the device has internet. That's it.

**The one exception:** If you want Wallet on Phone B to read from Node on Phone A, they need to be on the same WiFi. That's the only time WiFi location matters — for the wallet-to-node connection. Mining works anywhere regardless.

---

## How to Check if Mining Is Working

Open FootNode. Type:

    status

You'll see something like:

    Height: 4,062
    Peers: 3
    Your balance: 0.500000 FOOT

**What to look for:**

- **Height** — a number that goes up. If it's increasing, mining is working.
- **Peers** — how many other nodes you're connected to. 0 is OK. 1 or more is better.
- **Your balance** — the FOOT you've earned.

If the height isn't going up, something is wrong. Check the internet connection.

---

## What Happens if You Close the App

**On phone:**

- Fully close FootNode (swipe it away from recent apps) → mining stops until you open it again
- Leave it running in the background (just press home button) → mining continues

**To keep phone mining running 24/7:**

1. Open FootNode
2. Press the home button (don't swipe the app away)
3. Keep the phone plugged in
4. Turn off battery optimization for FootNode (Settings → Apps → FootNode → Battery → Unrestricted)

**On PC:**

- Close the terminal window → mining stops
- Leave the window open → mining continues
- Minimize the window → mining continues

For a PC that runs 24/7, just leave the window open. The computer will keep mining as long as it stays on.

---

## The Best Setup for Maximum Mining

If you want the most FOOT possible:

**Phone:**

1. Use an old phone that stays at home
2. Keep it plugged in — always on
3. Keep it on WiFi — no data usage
4. Set FootNode battery to Unrestricted — so it never gets killed
5. Leave the screen off — to save battery and reduce heat
6. Check `status` once a day — to confirm it's mining

**PC:**

1. Run FootNode on any computer that stays on
2. Leave the terminal window open
3. If on Linux or Mac, use `nohup` to keep it running in the background
4. Both the PC and the phone can mine to the same wallet

A phone and a PC together produce about 10 FOOT per day. That's twice the rate of one device.

---

## Commands You Can Use

Type any of these in the FootNode command bar (phone) or terminal (PC).

| Command | What it does |
|---|---|
| `start <address>` | Begin mining to an address |
| `stop` | Stop mining, keep the address |
| `stoptrack` | Stop mining and forget the address |
| `status` | Show node status and your balance |
| `balance <address>` | Show the balance of any address |
| `peers` | Show how many nodes you're connected to |
| `showip` | Show your local address (for two-phone setup) |
| `price` | Show the current floor price and reward rate |
| `vault` | Show the vault's balance and address |
| `fee <amount>` | Preview the fee for a transfer |
| `send <privateKey> <to> <amount>` | Send FOOT to another address |
| `backup` | Create an encrypted backup of your node |
| `restore` | Restore from a backup |
| `schedule` | See the reward decay story |
| `exit` | Close the app |

---

## Frequently Asked Questions

**Does WiFi cost extra?**
No. FootNode uses very little data. A full month of mining is less than 100 MB.

**Will this drain my battery?**
FootNode uses very little power. But keep the phone plugged in to be safe.

**Can I use my phone normally while mining?**
Yes. Mining runs in the background.

**Do I need to keep the screen on?**
No. Mining works with the screen off.

**What if my phone turns off?**
Mining stops. When you turn it back on, it resumes automatically (if you set battery to Unrestricted).

**Can I mine on my PC instead of a phone?**
Yes. The PC version mines the same way.

**Can I mine on PC and phone at the same time?**
Yes. Both work. Both produce FOOT. Both can mine to the same wallet.

**Does the PC version need a special setup?**
No. Install Java, download the file, run one command. That's it.

**Can the PC version and phone version talk to each other?**
Yes. They connect automatically over the internet. You don't configure anything between them.

**Can I use the PC version without a phone?**
You still need FOOT Wallet somewhere to see your balance and receive FOOT. The wallet is on a phone. But the mining can happen on the PC alone if you want — just point it at an address created by a wallet on any device.

**Can I mine on Phone A and check my balance on Phone B?**
Yes. Install FootNode on Phone A, install FOOT Wallet on Phone B. Both phones must be on the same WiFi. In the wallet on Phone B, open Settings and change the Host to Phone A's local address (run `showip` in FootNode to find it). Phone B's wallet now reads from Phone A's node.

**Can two phones on the same WiFi mine to one wallet?**
Yes. Set both phones to `start MFT-same-address`. Both mine to the same wallet. Wallet grows twice as fast.

**Does it matter if one phone is on WiFi and one is on mobile data?**
No. Both work. Both mine. Both connect.

**What if I have 10 devices?**
Same setup on all of them. Each mines. Each produces FOOT. All stay in sync.

**How do I know it's working?**
Type `status` in FootNode. If the height is going up, it's working.

**What if it's not working?**
Check the internet. Check that you ran `start <your-address>`. Check the log for errors.

**Can I lose my FOOT?**
Only if you lose your 12 words. Write them down. Keep them safe.

**Can someone steal my FOOT?**
Only if they get your 12 words or private key. Don't share them.

**How much does this cost?**
Nothing. FootNode is free. No fees to mine.

---

## The Rules

**DO:**
- Write down your 12 words
- Keep the paper safe
- Leave the phone plugged in
- Set battery optimization to Unrestricted
- Check status once a day

**DON'T:**
- Share your 12 words with anyone
- Share your private key with anyone
- Screenshot your 12 words
- Store them in email, notes, or cloud

If anyone asks for your 12 words or private key, they are trying to steal your FOOT. No exceptions.

---

## Quick Reference

**Start mining:**

    start MFT-your-address

**Stop mining (keep address):**

    stop

**Check status:**

    status

**See your peers:**

    peers

**Find your local address (for two-phone setup):**

    showip

**Exit the app:**

    exit

**Run on PC:**

    java -jar footnode.jar

---

**The whole thing in one sentence:**

Install FootNode and FOOT Wallet, create a wallet, type `start` with your address, leave the device on. FOOT comes slowly. The floor price rises. Done.

**Welcome to FOOT.**

