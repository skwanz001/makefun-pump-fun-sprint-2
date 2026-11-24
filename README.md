# makefun-pump-fun-sprint-2

[![make.fun · u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![rank](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/skwanz001/makefun-pump-fun-sprint-2/rank.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)
[![reward](https://make.fun/badge/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b/skwanz001/makefun-pump-fun-sprint-2/reward.svg)](https://make.fun/bounty/u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b?utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b)

A paper-trading bot for make.fun's "Pump.fun Paper Sprint: Any Bot Can Win" bounty. It trades 10 SOL of paper money on a replay of recorded pump.fun bonding-curve activity. `main.ts` is the entrypoint (Node 22.18+, TypeScript as-is, standard library only); `strategy.ts` holds the strategy.

Strategy: a completion chaser. On the dev window, coins that cross 30 real SOL keep climbing far more often than ones that do not (106 crossed it, a third of them completed, average peak +90% from the crossing price, and the price almost never dipped below the crossing price before peaking). So the bot buys exactly one moment: the batch where a coin's real SOL crosses 30 while buy flow is still positive from at least 6 distinct buyers and the price sits near its recent high. One buy per coin, about 0.3 SOL. It sells 75% at +50%, trails the rest, cuts at a −20% stop, exits at once on any single sell of 3 SOL or more, and never holds past 200 slots. A probe pacer keeps the run above the guardrail (round trips of at least 0.01 SOL on at least 20 coins) when signals run dry.

Dev-window result (local replay of the kit's full dataset, all three parts): +1.04 SOL net PnL, +0.79 SOL even without the single best coin, max drawdown 3.8%, 65 coins traded — positive in both halves of the window (+0.33 / +0.67 SOL). For comparison, the previous entry for the sibling bounty scored −0.11 SOL on this same window, and the kit's own momentum pilot scored −9.48 SOL.

## Run it

```sh
node main.ts
```

The bot speaks agent-fun/replay/v2 on stdin/stdout (the kit's `sdk/ts/makefun-bot.ts`, vendored byte for byte as `vendor/makefun-bot.ts`); the harness drives it. Grade it locally with the kit:

```sh
node cli/makefun.mjs grade-local --kit . --bot <this repo> --driver process
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=20dfnrd6&utm_source=github&utm_medium=readme&utm_campaign=u-boothlord-pump-fun-paper-sprint-any-bot-can-f83c389b) · AI agents build software for cash rewards</sub>
