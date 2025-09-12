# LeetCode 289 – Game of Life

## 🔎 Problem Understanding

We’re given an `m × n` grid (`board`) representing Conway’s Game of Life.  
Each cell can be:
- `1` → Alive
- `0` → Dead

**Task:**  
Update the board in-place to its next state by applying the rules **simultaneously**:

- **Underpopulation:** Live cell with fewer than 2 live neighbors → dies.
- **Survival:** Live cell with 2 or 3 live neighbors → lives on.
- **Overpopulation:** Live cell with more than 3 live neighbors → dies.
- **Reproduction:** Dead cell with exactly 3 live neighbors → becomes alive.

---

## ⚡ Key Challenge

We must **not overwrite cells prematurely**, since each cell’s next state depends on the current state of neighbors.

---

## 🛠 Optimal Approach (In-place with State Encoding)

We can update the board in-place by using extra state encoding:
- `0 → 0`: Dead → Dead
- `1 → 1`: Alive → Alive
- `1 → 2`: Alive → Dead (temporarily store as 2)
- `0 → -1`: Dead → Alive (temporarily store as -1)

When counting neighbors, use `Math.abs(board[x][y])` to get the original state.

### Steps

1. Iterate over each cell and count live neighbors.
2. Apply the rules:
   - If alive and should die → mark as `2`.
   - If dead and should become alive → mark as `-1`.
3. Traverse again to finalize → convert `2 → 0` and `-1 → 1`.

---

## ⏱ Complexity

- **Time Complexity:** O(m × n) → Each cell processed once.
- **Space Complexity:** O(1) → In-place update using encoded values.

---

## 💻 Java Code

```java
class Solution {
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1},{1,1},{1,-1},{-1,1},{-1,-1}};

        // First pass: compute next state using markers
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int liveNeighbors = 0;
                for (int[] d : dirs) {
                    int x = i + d[0], y = j + d[1];
                    if (x >= 0 && x < m && y >= 0 && y < n) {
                        // COUNT ORIGINAL live cells: originally alive are 1 or 2
                        if (board[x][y] == 1 || board[x][y] == 2) {
                            liveNeighbors++;
                        }
                    }
                }

                if (board[i][j] == 1) {
                    // live cell
                    if (liveNeighbors < 2 || liveNeighbors > 3) {
                        board[i][j] = 2; // was live, will die
                    }
                } else { // board[i][j] == 0
                    if (liveNeighbors == 3) {
                        board[i][j] = -1; // was dead, will become live
                    }
                }
            }
        }

        // Second pass: finalize states
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 2) board[i][j] = 0;
                else if (board[i][j] == -1) board[i][j] = 1;
            }
        }
    }
}
```
