# LeetCode 76 – Minimum Window Substring

## 🔎 Problem Understanding

We are given two strings:

- `s` → the source string  
- `t` → the target string

**Task:**  
Find the smallest substring of `s` that contains all characters of `t` (with frequency counts included).  
If no such substring exists, return an empty string `""`.

---

## ✅ Key Idea

This is a **Sliding Window + HashMap** problem.  
We expand and shrink a window over `s`, making sure the current window contains all characters of `t`.

---

## 🛠️ Optimal Algorithm (Sliding Window + Two Pointers)

1. Build a frequency map of all characters in `t`.
   - Example: for `t = "ABC"` → `{A:1, B:1, C:1}`

2. Use two pointers (`left` and `right`) to maintain a sliding window in `s`.

3. Expand `right` to include characters until the window contains all of `t`.

4. Once valid, shrink from `left` to minimize the window size.

5. Keep track of the minimum window substring seen so far.

6. At the end, return the substring if found, else return `""`.

---

## ⏱️ Complexity

- **Time Complexity:** O(m + n)  
  Each character in `s` is visited at most twice (once by `right`, once by `left`).
- **Space Complexity:** O(1)  
  (bounded by 128/256 possible ASCII chars).

---

## 💻 Java Code (Optimal Solution)

```java
import java.util.*;

class Solution {
    public String minWindow(String s, String t) {
        if (s.length() < t.length()) return "";

        // Frequency map for characters in t
        Map<Character, Integer> freqMap = new HashMap<>();
        for (char c : t.toCharArray()) {
            freqMap.put(c, freqMap.getOrDefault(c, 0) + 1);
        }

        int left = 0, right = 0;
        int required = freqMap.size(); // unique chars in t
        int formed = 0; // how many chars are satisfied in current window

        Map<Character, Integer> windowCounts = new HashMap<>();
        int minLen = Integer.MAX_VALUE;
        int start = 0;

        while (right < s.length()) {
            char c = s.charAt(right);
            windowCounts.put(c, windowCounts.getOrDefault(c, 0) + 1);

            // If the char count matches target count
            if (freqMap.containsKey(c) && windowCounts.get(c).intValue() == freqMap.get(c).intValue()) {
                formed++;
            }

            // Try to shrink the window when it's valid
            while (left <= right && formed == required) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    start = left;
                }

                // remove the leftmost character
                char lc = s.charAt(left);
                windowCounts.put(lc, windowCounts.get(lc) - 1);
                if (freqMap.containsKey(lc) && windowCounts.get(lc) < freqMap.get(lc)) {
                    formed--;
                }
                left++;
            }
            right++;
        }

        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}
```

---

✅ This solution is optimal with O(m + n) time.  
It’s a classic sliding window problem frequently asked in FAANG interviews.
