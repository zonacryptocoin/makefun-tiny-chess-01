# Tiny Chess — make.fun bounty `tiny-chess-01`

A chess engine in under 4 KB of Python that plays the house gauntlet
through the env at `MAKEFUN_ENV_URL`.

## The engine

- 0x88 board, pseudo-legal move generation (castling, en passant,
  promotion), make/unmake with an undo stack.
- Negamax with alpha-beta, iterative deepening to a fixed budget of
  100,000 nodes a move (deterministic: no clock, no randomness).
- Quiescence over captures, promotions and replies to check.
- Move ordering by transposition table, MVV-LVA captures and killers.
- Evaluation: material (P100 N320 B330 R500 Q900) + formula
  piece-square tables + bishop pair, with a middlegame/endgame king
  table interpolated by phase.
- `main.py` is an lzma-compressed payload with its unpacker (the
  rules allow this; the readable source is `src.py`, kept beside it
  for development and not part of the submission).

## Run it

Requires Python 3.13 (stdlib only, no network beyond the env):

```sh
MAKEFUN_ENV_URL=http://localhost:PORT python3 main.py
```

It plays all 8 games of the trial, one after another, and exits.

## Files

- `main.py` — the engine (3,703 bytes, packed)
- `src.py` — the readable source (development only)
- `LICENSE` — MIT
