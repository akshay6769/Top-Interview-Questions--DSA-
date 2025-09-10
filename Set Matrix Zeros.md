# LeetCode 73 – Set Matrix Zeroes

## 🔎 Problem Understanding

Given an `m x n` matrix, if any element is `0`, set its **entire row and column** to `0`.

**Catch:**  
Must do it **in-place** (without using extra space proportional to the matrix size).

---

## 🧠 Key Idea (Constant Space Solution)

Instead of extra arrays to track zero rows/columns, use the **first row and first column as markers**.

### ✅ Steps

1. **Check first row and first column separately**  
   (store two booleans: `firstRowZero`, `firstColZero`).  
   This is needed because they will be overwritten later.

2. **Mark rows & columns using first row/column:**  
   Traverse the matrix (except first row & column).  
   If `matrix[i][j] == 0`, mark `matrix[i][0] = 0` and `matrix[0][j] = 0`.

3. **Zero out based on markers:**  
   Traverse the rest of the matrix.  
   If either `matrix[i][0] == 0` OR `matrix[0][j] == 0`, set `matrix[i][j] = 0`.

4. **Handle first row & first column:**  
   If `firstRowZero == true`, set the entire first row to `0`.  
   If `firstColZero == true`, set the entire first column to `0`.

---

## ⏱ Complexity

- **Time Complexity:** O(m × n) → Each cell is visited a constant number of times.
- **Space Complexity:** O(1) → Only a few boolean flags are used.

---

## ✅ Optimized Java Code

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        boolean firstRowZero = false;
        boolean firstColZero = false;

        // Step 1: Check first column separately
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) 
                firstColZero = true;
        }

        // Step 2: Check first row separately
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) 
                firstRowZero = true;
        }

        // Step 3: Use first row/col as markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // Step 4: Set zeroes based on markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Step 5: Handle first row
        if (firstRowZero) {
            for (int j = 0; j < n; j++) 
                matrix[0][j] = 0;
        }

        // Step 6: Handle first column
        if (firstColZero) {
            for (int i = 0; i < m; i++) 
                matrix[i][0] = 0;
        }
    }
}
```

---

✅ Your implementation is already optimal (O(1) extra space) 🎉
