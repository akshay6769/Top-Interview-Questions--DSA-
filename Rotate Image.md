# LeetCode 48 – Rotate Image

## 🔎 Problem Restatement

Given an n x n 2D matrix (`image`), rotate the matrix **90° clockwise in-place** (without using extra space).

---

### 🧩 Example Walkthrough

**Example 1:**
```
Input:
1 2 3
4 5 6
7 8 9

After 90° clockwise rotation:
7 4 1
8 5 2
9 6 3
```

**Example 2:**
```
Input:
5   1   9   11
2   4   8   10
13  3   6   7
15 14  12   16

Output:
15  13   2   5
14   3   4   1
12   6   8   9
16   7  10  11
```

---

## ⚡ Optimal Approach (Transpose + Reverse Rows)

**Steps:**
1. **Transpose the matrix** (swap elements across the diagonal)
    - Example:
      ```
      1 2 3     1 4 7
      4 5 6 --> 2 5 8
      7 8 9     3 6 9
      ```
2. **Reverse each row** (to make it clockwise)
    - Example:
      ```
      1 4 7  →  7 4 1
      2 5 8  →  8 5 2
      3 6 9  →  9 6 3
      ```

**Why it works:**  
A 90° clockwise rotation is equivalent to transpose + reverse rows.

---

## ⏱️ Complexity

- **Time Complexity:** O(n²) (each cell visited once for transpose and once for row reversal)
- **Space Complexity:** O(1) (in-place, no extra matrix used)

---

## ✅ Java Code

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; i++) {
            int left = 0, right = n - 1;
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}
```
