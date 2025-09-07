🔎 Problem Understanding

We are given a 9×9 Sudoku board, partially filled.
We need to check whether it is valid under Sudoku rules:

Each row must have digits 1–9 without repetition.

Each column must have digits 1–9 without repetition.

Each 3×3 sub-grid must have digits 1–9 without repetition.

⚠️ Note: The board can be incomplete (with '.'), but all filled cells must satisfy these rules.

✅ Example
Example 1

Input:

[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]


Output: true ✅

Example 2

Same as above, but first element is 8 instead of 5.
Now, two 8s appear in the same 3×3 box → false.

⚡ Your Code Explanation

You used three validations:

Loop over rows → check duplicates.

Loop over columns → check duplicates.

Loop over each 3×3 sub-box → check duplicates using a helper validSub().

You stored values in a HashSet to detect duplicates.
👉 This works fine and runs in O(9×9) = O(1) time since the board is always 9×9.

🚀 Optimal Algorithm (Cleaner & More Efficient in One Pass)

Instead of checking rows, columns, and sub-boxes separately, we can do it in a single pass using sets:

For each cell (i, j) with value num:

Check if num already exists in:

row[i] set

col[j] set

box[i/3][j/3] set (maps to the right 3×3 sub-box)

If yes → invalid.

If no → add it.

🧑‍💻 Optimal Java Code
import java.util.*;

public class Solution {
    public boolean isValidSudoku(char[][] board) {
        // Use 9 hashsets for rows, cols, and boxes
        HashSet<Character>[] rows = new HashSet[9];
        HashSet<Character>[] cols = new HashSet[9];
        HashSet<Character>[] boxes = new HashSet[9];

        for (int i = 0; i < 9; i++) {
            rows[i] = new HashSet<>();
            cols[i] = new HashSet<>();
            boxes[i] = new HashSet<>();
        }

        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                char num = board[i][j];
                if (num == '.') continue;

                // Check row
                if (rows[i].contains(num)) return false;
                rows[i].add(num);

                // Check column
                if (cols[j].contains(num)) return false;
                cols[j].add(num);

                // Check 3x3 box (map to box index)
                int boxIndex = (i / 3) * 3 + (j / 3);
                if (boxes[boxIndex].contains(num)) return false;
                boxes[boxIndex].add(num);
            }
        }
        return true;
    }
}

⏱️ Complexity

Time Complexity: O(81) = O(1) (since board is fixed 9×9).

Space Complexity: O(81) = O(1) (sets store at most 81 elements).

✅ Your approach works fine. The optimized version just unifies everything in a single loop, which is cleaner and commonly asked in interviews.
