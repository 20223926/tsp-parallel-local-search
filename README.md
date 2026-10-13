# Parallel Local Search for the Traveling Salesman Problem

Master 1 research project (TER) on accelerating TSP heuristics through parallel local search and neighborhood hybridization.

## Overview

The Traveling Salesman Problem (TSP) is a classic NP-hard combinatorial optimization problem. Exact methods do not scale to large instances, so this project builds a practical heuristic pipeline that combines:

- **Nearest Neighbor** - greedy construction of an initial tour
- **2-opt** - sequential baseline, then batch improvement via conflict graphs and K-NN neighborhood reduction
- **3-opt** - parallel multi-process search over a reduced neighborhood
- **VNS** - Variable Neighborhood Search orchestrating 2-opt, 3-opt, and Double-Bridge (4-opt) kicks to escape local minima

Instances follow the **TSPLIB** standard (EUC_2D). Performance is evaluated with wall-clock time, solution gap to optimum, and parallel speedup.

## Project structure

| Path               | Role                                                                |
| ------------------ | ------------------------------------------------------------------- |
| `src/`             | Parsers, solvers (NN, 2-opt, 3-opt, VNS), benchmarks, visualization |
| `data/`            | TSPLIB instances (e.g. `berlin52.tsp`)                              |
| `tests/`           | Unit tests for each algorithmic step                                |
| `results/`         | Benchmark CSVs, figures, and analysis outputs                       |
| `requirements.txt` | Python dependencies                                                 |

## Approach

1. **Baseline** - TSPLIB parser, Nearest Neighbor, sequential 2-opt
2. **Batch 2-opt** - conflict-graph / MIS batching and K-NN pruning
3. **Parallel 3-opt** - neighborhood chunks distributed across CPU cores
4. **VNS** - hybrid metaheuristic with Double-Bridge perturbations
5. **Evaluation** - reproducible multi-run benchmarks on small to large TSPLIB instances
