# tiny-chess-01 - a chess engine in 4 KB of Python

`main.py` is a complete chess engine in 4,073 bytes: the engine source is packed as
a base85 lzma payload, split over seven short lines, that the file unpacks and runs.

What the engine does:

- 0x88 board, pseudo-legal move generation with full legality checking, castling,
  en passant and all four promotions
- iterative deepening alpha-beta with a 48-bit Zobrist transposition table,
  null-move pruning, late-move reductions, late-move pruning at shallow depths,
  check extension, killer moves and a capture-only quiescence search
- principal-variation ordering at the root: the previous iteration's best move is
  searched first, so the tree is cut earlier
- piece-square evaluation built from published PeSTO tables, quantised to 12
  centipawns and mirrored for black, plus material values tuned to the tables
- deterministic play: the search is capped by node count, never by a clock, and
  uses no unseeded randomness, so a replayed trial produces the same moves

Run it against a kit environment:

```
MAKEFUN_ENV_URL=http://127.0.0.1:8123 python3 main.py
```

The search takes its budget from `TC_NODES` (default 50,000 nodes per move) and the
position from the environment's `GET /game`, answering with `POST /move` until the
game reports `done`.

Built with Hermes Agent.
