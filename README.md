# 🧩 8-Puzzle Solver using Depth-First Search (DFS)

## 📌 Aim
The aim of this project is to implement a **Depth-First Search (DFS)** algorithm to solve the **8-puzzle problem**.
The program finds a path from a given **start state** to the **goal state** by exploring all possible moves systematically.

---

## 📌 Problem Statement
The **8-puzzle problem** consists of a 3x3 grid with tiles numbered `1–8` and one empty space (denoted by `0`).  
The objective is to **move the tiles** by sliding them into the empty space until the puzzle matches the **goal configuration**:


Given an initial state from the user, the program must:
1. Traverse the puzzle states using **DFS**.  
2. Record all visited states.  
3. Print the traversal order.  
4. Reconstruct and display the **final path** from start to goal.  

---

## 📌 Algorithm Used: Depth-First Search (DFS)

1. **Start with the initial state** and push it onto a stack.  
2. While the stack is not empty:  
   - Pop the top state.  
   - If the state has already been visited, skip it.  
   - Mark the state as visited.  
   - If it matches the goal state, terminate and reconstruct the path.  
   - Otherwise, generate all possible child states (by sliding the blank tile).  
   - Push unvisited child states onto the stack.  
3. If the stack becomes empty without reaching the goal, return **no solution**.  

---

## 📌 Code

import copy

class State:
    _id_counter = 0  

    def __init__(self, puzzle, parent_id=None):
        self.puzzle = puzzle
        self.parent_id = parent_id
        self.state_id = State._id_counter
        State._id_counter += 1

    def __str__(self):
        return "\n".join([" ".join(map(str, row)) for row in self.puzzle])

    def find_blank(self):
        for r in range(3):
            for c in range(3):
                if self.puzzle[r][c] == 0:
                    return r, c

    def get_possible_moves(self):
        moves = []
        row, col = self.find_blank()
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]  

        for dr, dc in directions:
            new_row, new_col = row + dr, col + dc
            if 0 <= new_row < 3 and 0 <= new_col < 3:
                new_puzzle = copy.deepcopy(self.puzzle)
                new_puzzle[row][col], new_puzzle[new_row][new_col] = new_puzzle[new_row][new_col], new_puzzle[row][col]
                new_state = State(new_puzzle, parent_id=self.state_id)
                moves.append(new_state)

        return moves

    def puzzle_to_tuple(self):
        return tuple(tuple(row) for row in self.puzzle)  


class PuzzleSolver:
    def __init__(self, start_puzzle, goal_puzzle):
        self.start_state = State(start_puzzle)
        self.goal_puzzle = goal_puzzle
        self.closed = set() 
        self.stack = [self.start_state]  
        self.state_map = {self.start_state.state_id: self.start_state}  
        self.visited_states = []  

    def solve(self):
        print("\n Goal State:")
        print(self.format_puzzle(self.goal_puzzle))
        print("=" * 20)

        while self.stack:
            current = self.stack.pop()
            current_key = current.puzzle_to_tuple()

            if current_key in self.closed:
                continue

            self.closed.add(current_key)
            self.visited_states.append(current)  

            if current.puzzle == self.goal_puzzle:
                print("\n Goal reached!\n")
                self.print_all_visited_states()
                self.print_final_path(current.state_id)
                return

            for neighbor in current.get_possible_moves():
                if neighbor.puzzle_to_tuple() not in self.closed:
                    self.stack.append(neighbor)
                    self.state_map[neighbor.state_id] = neighbor

        print(" No solution found.")

    def format_puzzle(self, puzzle):
        return "\n".join([" ".join(map(str, row)) for row in puzzle])

    def print_all_visited_states(self):
        print("\n DFS Traversal Path (Visited States in Order):\n")
        for i, state in enumerate(self.visited_states):
            print(f"Visited State {i} - State ID: {state.state_id}, Parent ID: {state.parent_id}")
            print(state)
            print("-" * 20)

    def print_final_path(self, goal_id):
        path = []
        while goal_id is not None:
            state = self.state_map[goal_id]
            path.append(state)
            goal_id = state.parent_id

        path.reverse()
        print("\nFinal Path from Start to Goal:")
        print(f"Path Length: {len(path)}\n")
        for i, state in enumerate(path):
            print(f"Step {i} - State ID: {state.state_id}, Parent ID: {state.parent_id}")
            print(state)
            print("-" * 20)




def take_user_input():
    print("Enter the 8-puzzle start state :")
    start = []
    for i in range(3):
        row = list(map(int, input(f"Row {i+1} : ").strip().split()))
        assert len(row) == 3, "Each row must contain exactly 3 numbers."
        start.append(row)
    return start

if __name__ == "__main__":
    start_puzzle = take_user_input()

    
    goal_puzzle = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 0]
    ]

    solver = PuzzleSolver(start_puzzle, goal_puzzle)
    solver.solve()

---

## 📌 Time and Space Complexity

### Time Complexity:
- In the worst case, DFS may explore **all possible states** of the 8-puzzle.  
- The total number of unique states = **9! = 362,880**.  
- Worst-case time complexity: **O(b^d)**  
  - where `b` = branching factor (≤ 4)  
  - `d` = depth of the solution.  

### Space Complexity:
- DFS uses a stack for storing states and a `closed set` for visited states.  
- Worst-case space complexity: **O(b·d)**, which is generally lower than BFS.  

---


