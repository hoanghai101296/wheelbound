# Wheelbound

The endless journey of Squeektoshi, written by the wheel, and a daily tactic game played on top of it.

[Squeekchain](https://squeekchain.com/) is a blockchain powered by a real hamster on a real wheel. Wheelbound turns that wheel's public, on-chain record into a story that every settled round moves forward, and lets you play each week against a boss that only the real running can defeat.

## The Raid Table (the game)

- Every wheel day (12:00 to 12:00 UTC, as Squeekchain counts it), everyone is dealt **the same three tactic cards**.
- Pick one before the wheel first turns that day. Squeektoshi's real running, shaped by your card, is the damage you deal to the week's boss. A day without a card deals only half.
- The cards were tuned on the real wheel's first week, so each averages about ×1.3 and the right one depends on how the night goes: **Night Owl** (×1.6 on running 22:00–02:00 UTC), **Early Bird** (×3.5 on running 04:00–09:00 UTC), **Marathon** (×1.7 on the longest unbroken run), **Sprint** (×3.5 on the fiercest half-hour), **Second Wind** (×3 on everything after the longest pause between runs), **Big Day** (×1.7 if today goes farther than yesterday, ×0.8 if not), **Lazy Day** (×1.7 if today stays shorter than yesterday, ×0.8 if not), **Steady Pace** (×1.3).
- Each finished day earns up to three stars, and Wheelbound reveals which card in the hand would have dealt the most. Today's score is shown live.
- Beat the boss's health ×1.4 by the end of the week to win the raid, then share the week as an emoji grid.
- Fair play: picks are checked against Squeekchain's own clock (not the computer's), and a pick made after the wheel first turned does not count.

## Wallet and Sepolia

- **Connect a wallet** (MetaMask, Rabby or any EIP-6963 wallet). Wheelbound asks to switch to Sepolia, where Squeekchain runs.
- **Signed picks.** With a wallet connected, every card pick is signed with a plain message (`personal_sign`): it is free and sends no transaction. Picks are kept per wallet; without a wallet you play as a guest on this device.
- **Your holdings.** The wallet bar shows the SQK balance and the number of Squeek NFTs the address holds, read straight from Sepolia.
- **Round by round.** Every settled 10-minute round is a hit on the boss, shaped by that day's card. Each hit links its settlement transaction on Sepolia, and Wheelbound reads that transaction back from Sepolia (public RPC) and checks that its SqueekCore log carries the same rounds and the same running total of work as the API before marking it ✓.

## The journey

- **The trail.** Squeektoshi's position is the real lifetime distance the wheel has turned (exactly 878 mm per unit of settled work). A landmark waits every 5 km and the land changes every 25 km, through eight lands from the Seed Meadows to the Moonlit Burrows.
- **The Chronicle.** Each wheel day becomes a chapter. Its words come from the settled rounds (when the wheel first turned, the longest unbroken run, the fiercest round, the naps), the landmarks reached, and Squeekchain's own milestone, streak and speed-record events.
- **A painting for every day.** An aurora lit by each half-hour of running, hills shaped by the day, the landmarks reached standing on the ridge, and a glowing path that climbs with the distance run.
- **A boss every week.** The week's distance is the damage Squeektoshi deals alone; the boss falls at the exact minute it runs out of health, or escapes when the week ends.
- **Stream overlay.** Add `#overlay` to the address for a transparent card (where Squeektoshi is, the next landmark, the boss's health) for an OBS browser source.

Every name, word and brush stroke is derived from settled chain data with a fixed seed, so everyone who opens Wheelbound reads the same story. Chapters can be saved as 1200×630 cards or copied as text.

## Data

All data is read in the browser from the public Squeekchain API at `https://api.squeekchain.com`:

| Endpoint | Used for |
|---|---|
| `/v1/status` (every 10 s) | live wheel state and today's distance |
| `/v1/core` | round configuration (genesis time, 600 s rounds) |
| `/v1/measurement/stats?range=30d` | the wheel-day boundary, recent half-hour buckets, lifetime distance |
| `/v1/events?category=protocol` | settled round history, read once and cached, then only the newest page; gaps are found and refilled on their own |
| `/v1/events?category=measurement` | distance milestones, streaks and speed records |
| Sepolia RPC (`eth_getTransactionReceipt`, `eth_call`) | checking settlements on SqueekCore, SQK and Squeek balances |

## Run locally

Static site, no build step: `index.html`, `favicon.svg` and `og.png` (the link preview). Serve the folder with any static server (for example `npx serve .`) and open the page.
