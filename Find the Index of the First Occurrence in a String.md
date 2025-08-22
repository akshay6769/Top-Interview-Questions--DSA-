# LeetCode 28 – Find the Index of the First Occurrence in a String

## 🔎 Problem

We are given two strings:

- **haystack** → the main string.
- **needle** → the substring we need to search.

We need to find the first index where `needle` occurs in `haystack`. If not found, return -1.

---

## ✅ Explanation of Your Code

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) {
            return 0;  // If needle is empty, return 0 by definition
        }

        int m = haystack.length();
        int n = needle.length();

        // Iterate through haystack until the remaining substring is at least as long as needle
        for (int i = 0; i <= m - n; i++) {
            
            // Take substring of haystack from i to i+n and compare with needle
            if (haystack.substring(i, i + n).equals(needle)) {
                return i; // Found needle at index i
            }
        }

        return -1; // If no match is found
    }
}
```

---

## ⚡ How It Works

- **Edge Case:** If `needle` is empty, return 0 (by definition of the problem).
- **Loop:** Check every possible substring of length `needle.length()` inside `haystack`.
- **Compare:** Use `substring(i, i+n)` and compare with `needle`.
- **Return:** The first index where match is found. If none, return -1.

---

## ⏱️ Time Complexity

- O((m-n+1) * n) worst case, where m = haystack.length() and n = needle.length().
- For each starting position, substring comparison takes up to n time.

## 📦 Space Complexity

- O(1) (ignoring substring temporary objects).

---

👉 This is a brute force but valid solution.  
For optimization, we can use KMP (Knuth-Morris-Pratt) algorithm which works in O(m+n) time, but your solution is simple and effective for most cases.
