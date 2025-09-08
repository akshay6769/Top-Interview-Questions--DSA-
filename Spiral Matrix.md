🔎 Problem Restatement

We are given an m x n matrix, and we need to traverse it in spiral order (clockwise) and return the sequence of elements.

🧩 Example Walkthrough
Example 1:
matrix = [[1,2,3],
          [4,5,6],
          [7,8,9]]


Spiral order → [1,2,3,6,9,8,7,4,5]

Example 2:
matrix = [[1,2,3,4],
          [5,6,7,8],
          [9,10,11,12]]


Spiral order → [1,2,3,4,8,12,11,10,9,5,6,7]

⚡ Optimal Approach (Simulation with Boundaries)

We use four pointers to keep track of the current boundaries of the spiral traversal:

top → starting row index

bottom → ending row index

left → starting column index

right → ending column index

Steps:

Traverse left → right across the top row, then increment top.

Traverse top → bottom down the right column, then decrement right.

If still valid, traverse right → left across the bottom row, then decrement bottom.

If still valid, traverse bottom → top up the left column, then increment left.

Repeat until all boundaries collapse.

⏱️ Complexity

Time Complexity: O(m * n) → Each element is visited once.

Space Complexity: O(1) (excluding result list).

✅ Java Code
import java.util.*;

class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        if (matrix == null || matrix.length == 0) return result;

        int top = 0, bottom = matrix.length - 1;
        int left = 0, right = matrix[0].length - 1;

        while (top <= bottom && left <= right) {
            // Traverse left → right
            for (int i = left; i <= right; i++) {
                result.add(matrix[top][i]);
            }
            top++;

            // Traverse top → bottom
            for (int i = top; i <= bottom; i++) {
                result.add(matrix[i][right]);
            }
            right--;

            // Traverse right → left (check if valid)
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    result.add(matrix[bottom][i]);
                }
                bottom--;
            }

            // Traverse bottom → top (check if valid)
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    result.add(matrix[i][left]);
                }
                left++;
            }
        }
        return result;
    }
}
