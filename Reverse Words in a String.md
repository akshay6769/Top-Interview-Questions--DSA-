# LeetCode 151 – Reverse Words in a String

## 🔎 Problem Understanding

We are given a string `s` with words separated by spaces (possibly multiple spaces, leading spaces, or trailing spaces).

**Tasks:**
- Reverse the order of words.
- Remove extra spaces (only one space should separate words).
- Remove leading and trailing spaces.

---

## 👉 Example
`s = " hello world "` → `"world hello"`

---

## ⚡ Key Insights

- We only reverse the order of words, not the letters inside a word.
- Handling extra spaces is crucial.
- The final result should be trimmed and clean.

---

## 🛠️ Optimal Algorithm (Step-by-step)

1. **Trim the string** → remove leading and trailing spaces.
2. **Split the string** by one or more spaces (`regex "\\s+"` handles multiple spaces).
3. **Reverse the array of words.**
4. **Join the words** with a single space `" "`.

---

## ⏱️ Time & Space Complexity

- **Time Complexity:** O(n) (we traverse the string once and reverse words).
- **Space Complexity:** O(n) (extra space for storing words array).

**Note:** The follow-up (in-place solution with O(1) extra space) is possible in languages like C++ using character arrays, but in Java strings are immutable, so O(n) space is fine.

---

## ✅ Java Code

```java
class Solution {
    public String reverseWords(String s) {
        // Step 1: Trim spaces from start and end
        s = s.trim();
        
        // Step 2: Split by one or more spaces
        String[] words = s.split("\\s+");
        
        // Step 3: Reverse the words
        StringBuilder result = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            result.append(words[i]);
            if (i > 0) result.append(" ");
        }
        
        return result.toString();
    }
}
```

---

## 🧪 Example Run

**Input:** `"a good example"`  
- After trimming: `"a good example"`
- After splitting: `["a", "good", "example"]`
- After reversing: `"example good a"`

**✅ Output:** `"example good a"`
