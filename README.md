# CCC_UTM_Classic_2026 - Team Solutions

Uploaded files from CCC 2026 42nd #Classic with our team solutions and test data.

## Theme of 42nd edition: Nanofabricator
In a cleanroom so clean that even the dust must wear a hairnet, Dr. Ångström switches on **FAB-42**, the world's first nanofabricator. It doesn't print, carve or mill anything: it creates matter with laser light, one hexagonal cell at a time. Six emitters ride on a rail around a hexagonal board; wherever exactly two laser beams cross, matter appears, and where three or more cross, matter is destroyed. The levels build FAB-42's software step by step: modelling the board, simulating emitter programs, detecting finished patterns, and finally (level 6, optimization) writing the shortest programs that produce each pattern the required number of times.

## Results
We solved all **6 levels** and finished with:
- **UTM (local): 1st place**
- **Global: 14th place**
- **Level 6 score: 14,566** total instruction lines, lower is better (medium 5,806 · large 4,664 · enormous 4,096)

## How level 6 was optimized
- C++ beam search over all 4,096 emitter moves per tick, deduplicating states on pattern cells only (`bs6s.cpp`, `bs6p.cpp`)
- GPU beam search with CuPy/CUDA at beam widths up to 131,072 (`gpu6.py`)
- Tail re-search from intermediate states of the best programs, on GPU and CPU (`tail6g*.py`, `tailA.py`, `post6.cpp`)
- Search rules relaxed to match the real game: rebuilding destroyed cells, temporary matter next to the pattern (`gpu6r.py`, `gpu6a.py`), plus a lower-bound rerank (`gpu6L.py`)
- Per-case merge of every candidate with an exact simulator/validator (`merge6.py`, `nano6.py`), with submissions automated through the contest API

## Repository structure
- `CCC.zip`: all contest files
  - `level_1/` … `level_5/`: statements, inputs, outputs and solutions
  - `level_6/`: statement, inputs and `opt/` with all solvers, tools and outputs (`w_*.out` are the final submitted programs)
