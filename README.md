# tiny-chess-01 entry

A chess engine in a single 4,096-byte Python file: 0x88 board, alpha-beta
negamax with capture quiescence, a transposition table, killer/history move
ordering, late-move reductions (LMR), check extensions, and a fixed node
budget (65,000 nodes per move, iterative deepening, no clock, so final
replays are deterministic). The evaluation is tapered material +
piece-square tables with pawn structure (isolated, doubled, passed) and
king safety (pawn shield, attacks on the king ring).

`main.py` is the compressed form of the readable `engine.py` source
(`makefun compress`, LZMA + base85; the source is bundled with the entry
for the transcript check and is not committed). Python 3.13, standard
library only; it reads no other file.

Local practice score (trial-2, kit scorer): Elo 1099 (1 win, 2 draws,
3 losses).

## Run it

It talks to the make.fun env over HTTP only:

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8765 python3 main.py
```

It plays the whole gauntlet through `POST /game` and `POST /move`, then
exits.

## Files

- `main.py` — the whole engine (<= 4,096 bytes)
- `LICENSE` — MIT
- `.makefun/freshness.json` — entry anchor (kit `init`)
- `.makefun/owner.json` — owner wallet address
