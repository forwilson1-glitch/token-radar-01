# token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/forwilson1-glitch/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/forwilson1-glitch/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

The best token launch radar: 198 pre-token protocols ranked by implied
value, from a sealed DefiLlama snapshot of 2026-11-14. The watchlist (40
protocols, TVL of at least $50M, no token on record) is the floor; the
board adds 20 protocols above the floor the house list leaves out and 138
below it, all passing the same screen.

## The model (radar-2)

Implied value is a peer-comps model, computed only from the snapshot:

    implied = round( tvl_usd x peerMultiple(category)
                     x (1 + clamp(change_7d, -40, 80) / 100 x 0.75)
                     x (0.70 + min(age_days, 1460) / 1460 x 0.50)
                     x (1 + 0.04 x min(chains - 1, 5)) )

`peerMultiple` is the trimmed median market-cap / TVL of the live-token
protocols in the category, shrunk toward the global median (pseudo-count
4) and clamped to [0.06, 1.25]. No protocol name is special-cased. Every
row carries a five-step farm plan with costs and times, and the dashboard
shows the peer comps behind each row's multiple.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json|directory>
```

The program reads the snapshot, writes `board.json` (198 rows) and
`data.js`, copies `dashboard/` and `screenshots/` to the output, and
writes `dossier.json`. Node 22, standard library only, no network.

---

<sub>Entered on [make.fun](https://make.fun/?ref=y7jz6ac1&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
