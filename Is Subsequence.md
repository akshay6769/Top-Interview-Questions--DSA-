# LeetCode 392 – Is Subsequence

## 🔎 Problem Explanation

We are asked to determine whether string `s` is a subsequence of string `t`.

**Subsequence definition:**  
You can delete some characters from `t` (possibly none) without changing the relative order of the remaining characters, and it should exactly form `s`.

### Example

- `s = "abc"`, `t = "ahbgdc"` → ✅ true (since "a", "b", "c" appear in order in t)
- `s = "axc"`, `t = "ahbgdc"` → ❌ false ("x" is missing)

---

## 🛠️ Optimal Algorithm (Two Pointers)

- Use two pointers:
  - `i` → to traverse `t` (the bigger string).
  - `j` → to traverse `s` (the smaller string).
- Traverse `t`:
  - If `t[i] == s[j]`, move both pointers forward.
  - Otherwise, move only `i` forward.
- At the end:
  - If `j == s.length()`, it means we found all characters of `s` in order inside `t` → return true.
  - Else return false.

---

## ⏱️ Complexity Analysis

- **Time Complexity:** O(m + n) → at most one pass through both strings.
- **Space Complexity:** O(1) → only two pointers used.

---

## ✅ Java Code (Correct & Optimal)

```java
public class Solution {
    public boolean isSubsequence(String s, String t) {
        int m = t.length();
        int n = s.length();
        int i = 0, j = 0;

        while (i < m && j < n) {
            if (t.charAt(i) == s.charAt(j)) {
                j++; // move in s if match found
            }
            i++; // always move in t
        }

        return j == n; // check if all chars of s were matched
    }
}
```

---

✅ This solution is already optimal using the two-pointer technique.  
It works efficiently even when `t` is large (10^4) and `s` is relatively small (≤100).
