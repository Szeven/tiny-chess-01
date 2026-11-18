# tiny-chess-01 — notes

Engine: 0x88 board, negamax alpha-beta with PVS, iterative deepening to a
fixed 120,000-node budget (never a clock), quiescence over captures,
promotions and check evasions, transposition table (search + quiescence),
MVV-LVA + killer ordering, null-move pruning (R=2), eval = material +
piece-square tables + bishop pair. Root avoids a third repetition when a
near-equal alternative exists. Packed entrypoint: `main.py`, 4,038 bytes
(limit 4,096), made by the kit's `makefun compress` from `engine.py`
(15,639 bytes, sha256 a4307f90...; source kept beside the repo, not committed).

Verification (local, kit env server, Python 3.12):
- Perft all OK on 5 positions incl. Kiwipete (depth 3 = 97,862) and
  castling/en-passant/promotion cases; mate-in-1 test picks Qxf7#.
- vs greedy 1-ply capturer: won both games by mate (as white and black).
- Practice trial 0 (80k nodes, pre-PVS): 1.0/6 — weak; PVS fixed it.
- Practice trial 0, PVS engine: 3.5/6, Elo 1,364 (W depth-2/3/4,
  D nodes-500k, L nodes-100k/250k).
- Practice trial 1, 120k nodes: 3.5/6, Elo 1,364 (W depth-2, nodes-100k;
  D depth-3/4, nodes-500k; L nodes-250k).
- Practice trial 1 re-run (repetition avoidance): 3.5/6, Elo 1,364.
- Mean practice Elo 1,364 (floor 1,154; house baseline sunfish ~1,365).
  No illegal move sent (0 HTTP 400s); worst move ~2.4 s (limit 10 s).
