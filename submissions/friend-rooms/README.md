# Friend Rooms

Walk your Rare Friend to a room door, then watch it play a ten-seat number table on its own: the highest number wins, and 10% of every pot is burned in the model.

**Builder:** [khunchan](https://github.com/khunchan) · **Contact:** GitHub [@khunchan](https://github.com/khunchan) · **Category:** Economy Potential (also relevant: Token Activity and Character Spotlight) · **SDK:** FriendSDK v0.1 (0.1.0)

[Source code](https://github.com/khunchan/friendsdk/tree/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms) · [Game README with rules, measurements and Future SDK support](https://github.com/khunchan/friendsdk/blob/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/README.md) · [Notices](https://github.com/khunchan/friendsdk/blob/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/NOTICE.md)

## What it is

A black-and-white isometric hall with four doors. **Room 100 RF** works; Room 1,000, 10,000 and 100,000 RF are locked and say they need future SDK support. Behind the working door your Friend sits at a table with nine simulated bots. Everyone gets a unique number from 1 to 100 and the highest number wins the pot. You choose how many games to play, confirm the SDK prompts once, and your Friend plays them all. Numbers open one by one, bots from the lowest up and your Friend's number last, then the table shows how far short you were ("Your 87 — 5 short of 92").

**Everything is simulated.** No RF, private key or transaction signature is needed. Every amount is labelled SIMULATED.

## Screenshots

![One round: the numbers open one by one, bots from the lowest up and the Friend last, then a win with HIGHEST! and +9 RF SIMULATED](https://raw.githubusercontent.com/khunchan/friendsdk/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/media/round.gif)

*One round at x1 speed: bots open from the lowest number up, the Friend's number opens last, then the win.*

| Hall with the working door and three locked doors | Table during the reveal (closed plates show ?) |
| --- | --- |
| ![The hall](https://raw.githubusercontent.com/khunchan/friendsdk/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/media/hall.png) | ![The table mid-reveal](https://raw.githubusercontent.com/khunchan/friendsdk/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/media/reveal.png) |
| **A win: HIGHEST! and +9 RF SIMULATED** | **Session receipt** |
| ![A win at the table](https://raw.githubusercontent.com/khunchan/friendsdk/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/media/win.png) | ![The session receipt](https://raw.githubusercontent.com/khunchan/friendsdk/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/media/receipt.png) |

*Captured from the game in the SDK's public runner with the SDK's mocked, read-only test wallet and its sample Friend #7730. The preview rolls are scripted (a loss, a win, a loss) so that a win can be shown; all amounts are simulated. The capture script is `capture-media.mjs` in the game folder.*

## How it uses Rare Friends

- **Character Spotlight (also relevant):** your own Generations NFT is the main character. It walks the hall and sits at the table, drawn from its canonical sprite (pixels never altered), labelled with its ID and SDK character family, and it reacts to wins and losses with effects drawn around the sprite.
- **Token Activity (also relevant):** the burn is part of every round. Ten tickets go into the pot, the winner takes 90% and 10% is burned in the model. Autoplay turns one confirmation into many rounds, and a session receipt shows tickets spent, prizes won and the modelled burn. SDK v0.1 does not burn RF, so this is a labelled model, not a claim of real burning.
- **Economy Potential (main category):** the game README describes how this becomes a real token economy: shared rooms held in a contract, one allowance to join, a keeper that starts full rooms, one Dice randomness per round, costs paid from the round fee with the remainder burned, and several ticket tiers. It also gives a minimum-ticket formula with an estimate, so the economics do not rest on a fixed price.

## Run it

Node.js 22+ on Linux or Ubuntu/WSL2, plus a browser wallet holding a hardwired Rare Friends Generations NFT (generation ≥ 1) on Robinhood mainnet (4663).

```sh
git clone https://github.com/khunchan/friendsdk.git
cd friendsdk
git checkout 936319191953a7ef4451800e3c76262b0ca2c440
npm ci
npm run dev:game -- games/friend-rooms
```

Open the printed URL (normally `http://localhost:4173`), connect your wallet and select your Friend. The SDK verifies ownership before play. No hosted demo is provided yet.

## Play

Move with WASD, arrow keys or click/tap. Walk to the **Room 100 RF** door and press E (or tap its label). Pick how many games to play, then confirm the SDK prompts: one to buy tickets and one to use them. Watch the table, choose x1, x2 or **Skip to summary**, or **Stop after this round** and **Resume** later. Open **Session receipt** when you like, and press **Collect winnings** to move prizes to your balance. Settings has mute and reduced motion, and everything stays inside the SDK's 960 × 640 container.

## Rules and rewards

Everything is simulated. The SDK preview wallet is fixed at 20 RF, so the room runs at 1/100 of its design size: a "Room 100 RF" ticket costs **1 RF** in the preview. One run is limited to 11 games by the SDK's prize backing (each ticket reserves 9 RF).

| Result | Chance | Prize |
| --- | ---: | ---: |
| Highest number | 10% (1,000 basis points) | 9 RF |
| Lower number | 90% (9,000 basis points) | 0 RF |

Expected reward: **0.90 RF per 1 RF ticket** (90% return). The table has 10 seats (your Friend and 9 simulated bots), so one seat in ten holds the highest number. The pot is 10 tickets: the winner takes 9 RF (90%) and 10% (1 RF) is burned in the model. The SDK ticket result decides your outcome first, and the table is then dealt to match it; the numbers and bots are presentation only.

**Measured:** 9.89% win rate over 10,000 preview plays (95% interval 9.32% to 10.49%), 989 wins, 8,901 RF returned on 10,000 RF spent (89.01%). The run uses the SDK preview client with a fixed seed and is reproducible with `node games/friend-rooms/simulate.mjs 10000 20260920`; a unit test pins these numbers.

## Future SDK support

Friend Rooms is a preview. A real version needs: shared rooms with real players, several ticket tiers, a room contract with one allowance, a keeper bot and unattended settlement, one Dice randomness per round, gas and randomness paid from the round fee with the remainder burned, reading shared room state from game code, rooms of up to 100 seats with ceil(participants / 10) winners, a larger preview wallet, and Friend traits (Scenery, Floor) as a style source. The game README explains [how real Friends would join rooms](https://github.com/khunchan/friendsdk/blob/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/README.md#how-real-friends-join-rooms), why a contract is better than a server, and the [minimum ticket size](https://github.com/khunchan/friendsdk/blob/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/README.md#minimum-ticket-size-estimate) formula.

The economics are a formula, not a fixed price: a room is viable while (gas + RNG fee in ETH) × ETH price ≤ 10% × seats × ticket × RF price. The fee first pays the round's costs and the rest is burned. As an estimate as of 2026-09-20 (ETH about $2,450, 100,000 RF about 0.128 ETH from a community tracker, round costs about $0.10 assumed), a ten-seat room needs about 32 RF per ticket, so 1 and 10 RF are not viable and 100 RF is (about 3× margin, about 68% of the fee burned).

## Checks and known issues

Run on 2026-09-20 with SDK v0.1 and Node.js 22: `npm test` (111 tests: 109 passed, 0 failed, 2 skipped because Foundry is not installed), `npm run typecheck`, `npm run check:games` and `npm run check:browser` (all SDK browser checks) pass. The game's own unit tests (9) and browser check pass at 1100 px and 360 px with the SDK's mocked, read-only wallet fixture. The builder played more than 40 games by hand with a real wallet and two Friends: Generation 2 (Cellular) and Generation 4 (Skeleton).

Known limits: the preview wallet is fixed at 20 RF (hence the 1/100 scale and 11 games per run); bots, the shared table and the burn are simulated; progress resets when the preview session ends; on a 360 px wide screen the SDK container is only 360 × 240, so the table is small. No trading, wearable NFTs, creator fees or live economy are included. Token Activity metrics are not claimed. Production publication needs separate Rare Friends review.

## Credits

Built on FriendSDK v0.1: its world renderer and scenery, canonical Generations sprites (read from the chain, never altered), sound kit and runtime. The pixel font, table scene, number plates, bot tokens, rules and code are original to this game. See the [notices](https://github.com/khunchan/friendsdk/blob/936319191953a7ef4451800e3c76262b0ca2c440/games/friend-rooms/NOTICE.md). AI-assisted build (Claude Code).
