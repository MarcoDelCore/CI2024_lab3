# CI2024_lab3 
## Sliding Puzzle Solver  

This solution implements an **A\* search algorithm** to solve sliding puzzles of varying sizes (3x3, 4x4, and 5x5). The algorithm uses a **combined heuristic** based on Manhattan Distance and Linear Conflict to efficiently guide the search toward the solution.

The functions **`available_actions`** and **`do_action`**, which handle valid tile movements and state transitions, are the ones proposed by Professor Squillero during the lectures.

## A* Algorithm Overview  

The A* algorithm is a graph search method that balances exploring the lowest-cost path so far (**g(n)**) with estimating the remaining cost to the goal (**h(n)**). In this implementation:  

- **g(n)**: Tracks the cost (number of moves) taken to reach a state.  
- **h(n)**: Combines two heuristics:  
  1. **Manhattan Distance**: Measures the sum of vertical and horizontal distances of each tile from its goal position.  
  2. **Linear Conflict**: Adds penalties for tiles in their correct row/column but out of order, as resolving these requires additional moves.  

### Heuristic Details  

#### Manhattan Distance  
This heuristic calculates the direct distance of each tile to its goal position without considering obstacles.  

#### Linear Conflict  
Linear Conflict identifies tiles that are in their correct row or column but are blocked by others, causing additional moves to resolve. For example:  

Row: `[1, 3, 2]`  
- Tiles `3` and `2` are in their goal row but out of order, requiring one extra move to swap them.  
- The heuristic adds **2 moves per conflict** to the Manhattan Distance.  

By combining these, the heuristic is admissible and ensures the A* search remains efficient.  

## Metrics  

The following metrics are displayed after solving each puzzle:  
- **Number of Moves**: The length of the solution path.  
- **Execution Time**: Total time taken to find the solution.  
- **Evaluated Actions**: Total valid actions considered during the search.  

##  Limitations

While the A* algorithm with the combined heuristic is highly efficient for small puzzles, the following limitations apply:

- **Scalability**: Solving puzzles larger than 5x5 becomes computationally expensive due to the exponential growth of the state space.
- **Optimality**: The algorithm guarantees the optimal solution only if the heuristic is admissible.

## Results  

The following are the results of solving 3x3, 4x4, and 5x5 sliding puzzles using the implemented A* algorithm.  

---

### 3x3 Puzzle  

**Initial State**:
$\begin{bmatrix} 1 & 7 & 8 \\ 3 & 0 & 6 \\ 5 & 2 & 4 \end{bmatrix}$

**Goal State**:
$\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 0 \end{bmatrix}$

**Moves**: 26  
**Time**: 0.31 seconds  
**Evaluated Actions**: 284_206  

---

### 4x4 Puzzle  

**Initial State**:
$\begin{bmatrix} 4 & 9 & 11 & 3 \\ 12 & 8 & 1 & 5 \\ 0 & 7 & 15 & 10 \\ 2 & 13 & 6 & 14 \end{bmatrix}$ 

**Goal State**:
$\begin{bmatrix} 1 & 2 & 3 & 4 \\ 5 & 6 & 7 & 8 \\ 9 & 10 & 11 & 12 \\ 13 & 14 & 15 & 0 \end{bmatrix}$  

**Moves**: 72  
**Time**: 0.50 seconds  
**Evaluated Actions**: 319_959  

---

### 5x5 Puzzle  

**Initial State**:
$\begin{bmatrix} 24 & 8 & 2 & 15 & 16 \\ 22 & 18 & 1 & 3 & 10 \\ 13 & 12 & 0 & 7 & 23 \\ 21 & 6 & 19 & 9 & 17 \\ 20 & 14 & 11 & 4 & 5 \end{bmatrix}$  

**Goal State**:
$\begin{bmatrix} 1 & 2 & 3 & 4 & 5 \\ 6 & 7 & 8 & 9 & 10 \\ 11 & 12 & 13 & 14 & 15 \\ 16 & 17 & 18 & 19 & 20 \\ 21 & 22 & 23 & 24 & 0 \end{bmatrix}$  

**Moves**: 124  
**Time**: 62.94 seconds  
**Evaluated Actions**: 737_413  

---

### Observations  

- **3x3 Puzzle**: Solved quickly, with relatively few moves and evaluated actions.  
- **4x4 Puzzle**: More challenging, requiring more moves and actions but still manageable in time.  
- **5x5 Puzzle**: The computational cost increases significantly, demonstrating the exponential growth of the state space and the challenge of scaling the algorithm to larger puzzles.  
