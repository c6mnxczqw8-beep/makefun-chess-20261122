[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/c6mnxczqw8-beep/makefun-chess-20261122/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/c6mnxczqw8-beep/makefun-chess-20261122/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# Tiny chess engine (make.fun tiny-chess-01)

A chess engine in at most 4,096 bytes of Python. `main.py` is an
lzma-compressed payload with a small unpacker (the competition counts the
packed bytes); it expands to a self-contained engine that plays the whole
gauntlet through the env at `MAKEFUN_ENV_URL`.

Design: 120-square board kept from the side-to-move point of view (the
board is rank-flipped and case-swapped after every move), full legal move
generation (castling, en passant, promotions), incremental
material + piece-square evaluation with a bishop-pair bonus, negamax with
alpha-beta pruning, iterative deepening under a fixed node budget (never
a clock, so replays match), a transposition table, null-move pruning,
late-move reduction for quiet moves, check extensions, and a quiescence
search over captures and check evasions. Repetition and the fifty-move
rule score as draws inside the search.

Development: the engine was revised over recorded sessions, driven by
local tests (perft, incremental-eval consistency, determinism checks and
equal-budget self-play matches). Late-move reduction and the bishop-pair
term were each added only after the revised engine outscored the previous
version in head-to-head matches at the same 60,000-node budget.
