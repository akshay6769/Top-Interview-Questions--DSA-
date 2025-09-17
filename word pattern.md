# LeetCode 290 – Word Pattern

## 🔎 Problem Restatement

Given:
- A `pattern` (string of characters)
- A string `s` (sequence of words separated by spaces)

**Check if there exists a bijection (one-to-one mapping):**
- Each letter in `pattern` ↔ one unique word in `s`
- Each word in `s` ↔ one unique letter in `pattern`

If such mapping holds, return `true`, else `false`.

---

### 🧩 Example Walkthrough

**Example 1:**  
pattern = "abba"  
s = "dog cat cat dog"  
Mapping:  
- 'a' → "dog"  
- 'b' → "cat"  
Works perfectly.  
**Answer:** true

**Example 2:**  
pattern = "abba"  
s = "dog cat cat fish"  
Mapping:  
- 'a' → "dog"  
- 'b' → "cat"  
But last 'a' should map to "dog", but we got "fish".  
**Answer:** false

**Example 3:**  
pattern = "aaaa"  
s = "dog cat cat dog"  
Mapping:  
- 'a' → "dog" (ok first time)  
But next 'a' maps to "cat" → conflict.  
**Answer:** false

---

## ⚡ Optimal Algorithm (HashMap + Set)

1. Split `s` into words.  
   If length of words ≠ length of pattern → return false.

2. Use a `HashMap<Character, String>` to store char → word mapping.

3. Use a `HashSet<String>` to ensure no two chars map to the same word.

4. Iterate through pattern and words:
   - If char already mapped → check if it matches current word. If not, return false.
   - If char not mapped but word already mapped to another char → return false.
   - Otherwise, create new mapping.

5. If no conflicts → return true.

---

## ⏱ Complexity

- **Time:** O(n) where n = number of words = length of pattern.
- **Space:** O(n) for HashMap + HashSet.

---

## ✅ Java Code

```java
import java.util.*;

class Solution {
    public boolean wordPattern(String pattern, String s) {
        String[] words = s.split(" ");
        if (pattern.length() != words.length) return false;

        Map<Character, String> map = new HashMap<>();
        Set<String> usedWords = new HashSet<>();

        for (int i = 0; i < pattern.length(); i++) {
            char c = pattern.charAt(i);
            String word = words[i];

            if (map.containsKey(c)) {
                if (!map.get(c).equals(word)) {
                    return false; // mismatch in mapping
                }
            } else {
                if (usedWords.contains(word)) {
                    return false; // word already assigned to another char
                }
                map.put(c, word);
                usedWords.add(word);
            }
        }
        return true;
    }
}
```
