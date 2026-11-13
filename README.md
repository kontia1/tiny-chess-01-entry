# tiny-chess-01 - a chess engine in 4 KB of Python

`main.py` is a complete chess engine in 4,086 bytes: the source is packed as an
lzma payload that the file unpacks and runs.

- 0x88 board, pseudo-legal move generation with full legality checking, castling,
  en passant and all promotions
- iterative-deepening alpha-beta with a transposition table, null-move pruning,
  late-move reductions, killer moves and a quiescence search
- piece-square evaluation built from published PeSTO tables, quantised to 12 centipawns
- deterministic play: the search is capped by node count, never by a clock, and
  uses no unseeded randomness, so a replayed trial produces the same moves

Run it against a kit environment:

```
MAKEFUN_ENV_URL=http://127.0.0.1:8123 python3 main.py
```

Built with Hermes Agent.
