# LeetCode 6 – Zigzag Conversion

## 🔎 Problem Understanding

We need to rearrange characters of a given string `s` in a zigzag pattern across `numRows`, and then read row by row.

### 👉 Example:
```
s = "PAYPALISHIRING", numRows = 3

P   A   H   N
A P L S I I G
Y   I   R

Read row by row → "PAHNAPLSIIGYIR"
```

---

## ⚡ Key Observations

- If `numRows == 1` or `numRows >= s.length()`, the string remains unchanged.
- Zigzag traversal has a downward direction and then an upward diagonal direction.
- Each character is appended to its respective row.

---

## 🛠️ Optimal Algorithm

1. Handle edge cases: if `numRows == 1` → return `s`.
2. Use a `StringBuilder[]` array of size `numRows` to collect characters row by row.
3. Traverse the string:
   - Append the character to the current row.
   - Switch direction when reaching the top or bottom row.
4. Combine all rows into a single string.

---

## ✅ Code in Java

```java
class Solution {
    public String convert(String s, int numRows) {
        // Edge case
        if (numRows == 1 || s.length() <= numRows) {
            return s;
        }
        
        // Create StringBuilders for each row
        StringBuilder[] rows = new StringBuilder[numRows];
        for (int i = 0; i < numRows; i++) {
            rows[i] = new StringBuilder();
        }
        
        int curRow = 0;
        boolean goingDown = false;
        
        // Traverse the string
        for (char c : s.toCharArray()) {
            rows[curRow].append(c);
            
            // Change direction when hitting top/bottom
            if (curRow == 0 || curRow == numRows - 1) {
                goingDown = !goingDown;
            }
            
            curRow += goingDown ? 1 : -1;
        }
        
        // Combine all rows
        StringBuilder result = new StringBuilder();
        for (StringBuilder row : rows) {
            result.append(row);
        }
        
        return result.toString();
    }
}
```

---

## 📊 Complexity Analysis

- **Time Complexity:** O(n) → Each character processed once.
- **Space Complexity:** O(n) → We use extra space to store rows before merging.
