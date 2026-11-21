# tiny-chess

A chess engine in 4 KB of Python (3.13 stdlib only) for the make.fun contest
"Build the strongest chess engine in 4 KB of Python" (tiny-chess-01).

## Design

- Sunfish-style mailbox board (120-char string) with the rotate trick.
- PeSTO middlegame evaluation (tapered mg tables, file-mirrored and packed
  as 8-bit values).
- Alpha-beta with iterative deepening by a fixed node budget (100,000
  nodes/move), transposition table with bounds, quiescence search (captures
  only + stand pat), null-move pruning, LMR on quiet moves, move ordering
  (TT move first, then value-sorted), and contempt to avoid repetition
  draws against weaker opponents.
- The root only searches legal moves (king-capture probe) and the returned
  move is verified against the environment's legal move list, so it never
  sends an illegal move.
- Deterministic: fixed node count, no wall-clock time, no unseeded
  randomness. The engine talks to the make.fun environment over HTTP
  (`MAKEFUN_ENV_URL`).

## Files

- `main.py` — the whole engine, self-extracting (lzma + base85). 4,077 bytes.
- `README.md`, `LICENSE` — this file and the MIT license.

## Inspiration

The mailbox board and search structure are inspired by Thomas Ahle's
[sunfish](https://github.com/thomasahle/sunfish). All code here is original,
written for this contest; no sunfish source was copied.

## License

MIT. See `LICENSE`.
