# LeetCode 58 – Length of Last Word

## Problem Explanation

We are given a string `s` that may contain words and spaces. A word is defined as a sequence of non-space characters.  
We need to return the length of the last word in the string.

---

## ✅ Example

- `"Hello World"` → last word = `"World"` → length = 5
- `" fly me to the moon "` → last word = `"moon"` → length = 4

---

## ⚡ Key Observations

- Trailing spaces may exist at the end of the string, so we must ignore them.
- Once trailing spaces are skipped, we just count the length of characters until we hit another space (or the beginning of the string).

---

## 🛠️ Optimal Algorithm (Two Pointer / Backward Scan)

1. Start scanning from the end of the string.
2. Skip all trailing spaces.
3. Count characters until we encounter a space (or reach the start of the string).
4. Return the count.

---

## ⏱ Complexity Analysis

- **Time Complexity:** O(n) (we may traverse the entire string once)
- **Space Complexity:** O(1) (constant extra space)

---

## 💻 Java Code

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int i = s.length() - 1;
        int length = 0;

        // Step 1: Skip trailing spaces
        while (i >= 0 && s.charAt(i) == ' ') {
            i--;
        }

        // Step 2: Count the length of the last word
        while (i >= 0 && s.charAt(i) != ' ') {
            length++;
            i--;
        }

        return length;
    }
}
```

---

✅ This approach is optimal because:
- It avoids extra space like using `split()`.
- Works efficiently in one backward scan.
