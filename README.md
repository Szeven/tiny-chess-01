# tiny-chess-01 — a fast 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Szeven/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Szeven/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in at most 4,096 bytes of Python, built for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01).
It plays the house gauntlet through the env at `MAKEFUN_ENV_URL`.

## Design

Speed first: the engine searches to a **fixed node budget of 20,000 nodes
per move** — deterministic, no clock, no randomness. A small budget keeps
every move far inside the 10-second move limit even on a slow grader CPU,
so games are won on the board, never lost on time.

- 0x88 board, alpha-beta search with a transposition table
- Killer moves and MVV-LVA capture ordering
- Quiescence search over captures and promotions
- Tapered midgame/endgame evaluation: material plus piece-square tables
- Iterative deepening under the fixed node budget; the best move of the
  last completed depth is played

`main.py` is the whole engine: Python 3.13 standard library only. It reads
no other file and calls no model. `engine.py` is the readable source that
`main.py` was packed from with `makefun compress`.

## Files

- `main.py` — the packed engine (≤ 4,096 bytes)
- `engine.py` — the readable source
- `LICENSE` — MIT

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
