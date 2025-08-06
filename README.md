**8-Puzzle Solver using BFS and DFS**

**Aim** :  The objective of this code is to implement a Python-based solution to the 8-puzzle problem, using two classic uninformed search strategies — Breadth-First Search (BFS) and Depth-First Search (DFS).

Given any solvable 3×3 configuration of the 8-puzzle, the program aims to find a sequence of valid moves to reach the goal state, while also demonstrating the path followed by the algorithm and all intermediate states explored in the process.

**Problem Statement**

The 8-puzzle consists of a 3x3 grid containing 8 numbered tiles and one blank space (represented by 0). The tiles can be slid into the blank space to rearrange them. The challenge is to transform a given initial state of puzzle into the goal state. The tiles can be moved up, down, left, or right into the blank, and the puzzle is solved when the current state matches the goal state.

**Algorithms Used**

**1. Depth-First Search (DFS)**
  
Approach:
DFS explores as deep as possible into the state space before backtracking. It follows one path until it can't go further, then explores alternatives.

Implementation Highlights:

Uses a stack (LIFO) for state exploration.

Keeps track of visited states in a closed list to avoid infinite loops.

Uses a parent ID system to reconstruct the final path.

Drawback:
DFS does not guarantee the shortest path and may go deep into less optimal paths.

**2.  Breadth-First Search (BFS)**

Approach:
BFS explores the state space level by level, ensuring that the shallowest (and thus shortest) solution is found first.

Implementation Highlights:

Uses a queue (FIFO) for state exploration.

Like DFS, maintains a closed list and parent linkage for path reconstruction.

Guarantees the shortest solution path (in terms of number of moves).

Trade-off:
BFS consumes more memory than DFS due to storing a wider set of states at each level.


**Algorithm: 8-Puzzle Solver using Depth-First Search (DFS)**

Initialization :Accept the start state (3x3 matrix) from the user.
   
2.Define the goal state 

3.State Representation Each state stores:

The 3x3 puzzle configuration.

A unique state_id and its parent_id.

A method to generate all possible next states by moving the blank tile (0) in four directions: up, down, left, and right (if valid).

4. DFS Traversal :
Use a stack to perform DFS.

Use a closed set to track visited configurations and avoid revisiting.

At each step:

Pop a state from the stack.

If it matches the goal state:

Print the DFS traversal path.

Reconstruct and print the final path using parent IDs.

Exit.

Otherwise:

Generate all valid next moves.

Push unvisited neighbors onto the stack.

5. Output
If the goal is found, print:

All visited states in DFS order.

The final path from the start to the goal.

If not found, print a message: "No solution found."

**Algorithm: 8-Puzzle Solver using Breadth-First Search (BFS)**
1. Initialization
Accept the start state (3x3 matrix) from the user.

Define the goal state

2. State Representation
Each state stores:

The 3x3 puzzle configuration.

A unique state_id and its parent_id.

A method to generate all valid next states by sliding the blank tile (0) in one of four directions: up, down, left, or right.

3. BFS Traversal
Use a queue (FIFO) to perform BFS.

Use a closed set to keep track of visited puzzle configurations and avoid loops.

While the queue is not empty:

Dequeue the current state.

If it matches the goal state:

Print the BFS traversal path.

Reconstruct and print the final path using parent IDs.

Exit.

Otherwise:

Generate all valid next moves.

Enqueue unvisited neighbors.

Store each neighbor in a state_map using its state_id.

4. Output
If the goal is found, display:

All visited states in BFS order.

The path from the start state to the goal state (with step-by-step board configuration).

If the goal is not found, print: "No solution found."


**Comments on Time & Space Complexity**

Time and space complexity for both the DFS and BFS implementations of the 8-puzzle solver:

DFS (Depth-First Search):

Time Complexity: O(b^d)

b = branching factor (max 4 in the 8-puzzle)

d = maximum depth of the search tree

In the worst case, DFS may explore all possible states (up to ~181,440 for 8-puzzle), especially if the goal state is deep or located at the last branch.

Note: DFS does not guarantee shortest path and can go very deep.

Space Complexity: O(d)

DFS uses a stack, so it only needs to store nodes in the current path and a visited set.

Space usage is linear with depth, not with the number of states.

Much better than BFS in terms of memory for deep trees.

Summary 
 Good for memory-constrained environments.

 May not find shortest solution.

 Can get trapped in deep or looping paths if not managed carefully.

BFS (Breadth-First Search)

Time Complexity: O(b^d)

b = branching factor (max 4)

d = depth of the shallowest goal state

BFS explores level-by-level, so time complexity depends on the depth at which the goal is found.

In the worst case, BFS may also explore all ~181,440 states.

Space Complexity: O(b^d)
BFS stores all nodes at the current level in memory (in the queue and visited set).

This can be very memory-intensive as the number of nodes grows exponentially with depth.

Summary 
 Always finds the shortest solution (optimal).

 High memory usage.

 Becomes infeasible for puzzles with deeper solutions.


💡 Use Cases
1.AI Learning & Education: Great for understanding how uninformed search algorithms work in AI and pathfinding.

2.Game Development :Core logic for creating tile-based puzzle games or brain-teasers.

3.Robotics & Path Planning: Can be extended to solve real-world movement/path problems in constrained environments.

4.Interview Preparation: Classic problem often asked in data structures & algorithms interviews.

5.Heuristic Algorithm Testing: Serves as a foundation for comparing with heuristic-based methods like A*, IDA*, etc.

**How the Program Works**

Input: User is prompted to enter the initial 3x3 matrix configuration.

Processing:

1.States are represented as objects with unique IDs and parent tracking.

2.The selected algorithm (DFS or BFS) explores the state space.

3.All states visited are printed.

4.The final path from initial to goal state is reconstructed and displayed.

Output:

1.Goal state.

2.Path taken to reach the goal.

3.All intermediate visited states (to illustrate algorithm traversal).


📂 Code by: Komalpreet kaur

📅 Date: 06-08-2025

📘 Subject: Artificial Intelligence Lab / Problem Solving using Search

