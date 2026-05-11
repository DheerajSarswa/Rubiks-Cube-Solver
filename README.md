# Rubik's Cube Solver

A high-performance C++ implementation of a Rubik's Cube solver with multiple search algorithms and cube representations. This project provides efficient solutions to the 3x3 Rubik's Cube using various search strategies and pattern databases for optimization.

## Features

- **Multiple Cube Representations**
  - 3D Array representation
  - 1D Array representation
  - Bitboard representation (space-efficient)

- **Multiple Solving Algorithms**
  - Depth-First Search (DFS)
  - Breadth-First Search (BFS)
  - Iterative Deepening Depth-First Search (IDDFS)
  - Iterative Deepening A* (IDA*) with heuristics

- **Performance Optimization**
  - Pattern Databases for heuristic evaluation
  - Corner permutation indexing
  - Efficient nibble-based storage for pattern databases
  - Benchmark-ready implementations to compare performance

- **Cube Scanning**
  - OpenCV-based physical cube scanner for real-world integration

## Project Structure

```
.
├── Model/                           # Cube representation models
│   ├── RubiksCube.h/cpp            # Base class with shared functionality
│   ├── RubiksCube3dArray.cpp       # 3D array representation
│   ├── RubiksCube1dArray.cpp       # 1D array representation
│   ├── RubiksCubeBitboard.cpp      # Bitboard representation
│   └── PatternDatabase/            # Pattern database interfaces
├── Solver/                          # Solving algorithms
│   ├── DFSSolver.h                 # Depth-First Search
│   ├── BFSSolver.h                 # Breadth-First Search
│   ├── IDDFSSolver.h               # Iterative Deepening DFS
│   └── IDAstarSolver.h             # A* with pattern database heuristics
├── PatternDatabases/               # Pattern database utilities
│   ├── CornerPatternDatabase.h/cpp # Corner piece pattern database
│   ├── CornerDBMaker.h/cpp         # Pattern database generator
│   ├── NibbleArray.h/cpp           # Compact array storage
│   ├── PermutationIndexer.h        # Permutation indexing
│   └── math.h/cpp                  # Mathematical utilities
├── Scanner/                         # Cube scanning
│   ├── CubeScanner.h/cpp           # OpenCV-based scanner
└── Databases/                       # Pre-computed databases
    └── cornerDepth5V1.txt          # Corner pattern database
```

## Requirements

- C++14 or higher
- CMake 3.20 or later
- OpenCV (for cube scanning features)
- Standard C++ library

## Building

### Prerequisites

Install OpenCV:

```bash
# macOS (using Homebrew)
brew install opencv

# Ubuntu/Debian
sudo apt-get install libopencv-dev

# Other systems - follow OpenCV installation guide
```

### Build Steps

```bash
cd rubiks-cube-solver-main
mkdir build
cd build
cmake ..
make
```

The compiled executable will be located at `build/rubiks_cube_solver`.

## Usage

Run the solver:

```bash
./build/rubiks_cube_solver
```

## Supported Moves

The solver supports standard Rubik's Cube notation:

- **Face moves**: U, D, L, R, F, B (90° clockwise)
- **Prime moves**: U', D', L', R', F', B' (90° counter-clockwise)
- **Double moves**: U2, D2, L2, R2, F2, B2 (180°)

Where:

- U = Up
- D = Down
- L = Left
- R = Right
- F = Front
- B = Back

## Algorithms

### DFS (Depth-First Search)

Simple tree search that explores as far as possible along each branch before backtracking.

### BFS (Breadth-First Search)

Explores all states at the current depth before moving to deeper levels. Guarantees shortest solution path.

### IDDFS (Iterative Deepening DFS)

Combines DFS's space efficiency with BFS's optimality guarantee. Performs depth-limited DFS with incrementally increasing depth limits.

### IDA* (Iterative Deepening A*)

Enhances IDDFS with admissible heuristics from pattern databases. Uses corner permutation patterns to estimate distance to goal state, significantly improving search efficiency.

## Implementation Details

### Cube Representations

- **3D Array**: Intuitive representation using 3D coordinates
- **1D Array**: Linear representation for memory efficiency
- **Bitboard**: Highly efficient bit-level representation using bitwise operations

Each representation can be benchmarked to determine which performs best for different solving algorithms.

### Pattern Databases

The IDA\* solver uses pre-computed pattern databases containing optimal distances for corner piece configurations. This provides admissible heuristics that significantly prune the search space.

## Author & Contributors

- Created by Lakshya Mittal (17-12-2021)
- Modified by Pranav Harresh (25-07-2025)
- Co-creator: Shubham Patil (17/12/21)

## License

[Add appropriate license information]

## Notes

- The project is designed for benchmarking and comparing different search algorithms
- Pattern databases are pre-computed for faster solving with IDA\*
- Multiple cube representations allow for performance comparison
- Template-based design allows reuse with different cube representations and hash functions
