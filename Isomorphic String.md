# LeetCode 205 – Isomorphic Strings

## 🔎 Problem Restatement

Given two strings `s` and `t`, determine if they are **isomorphic**:
- Characters in `s` can be replaced to form `t`.
- The order of characters must be preserved.
- No two characters in `s` can map to the same character in `t`.
- A character can map to itself.

---

### 🧩 Example Walkthrough

- **Example 1:**  
  s = "egg", t = "add" → ✅ True  
  Mapping: e → a, g → d

- **Example 2:**  
  s = "foo", t = "bar" → ❌ False  
  Mapping breaks since o would need to map to both a and r.

- **Example 3:**  
  s = "paper", t = "title" → ✅ True  
  Mapping: p → t, a → i, e → l, r → e

---

## ⚡ Optimal Algorithm (HashMap Based)

Use two HashMaps for one-to-one mapping:
- `mapST`: maps characters from `s → t`
- `mapTS`: maps characters from `t → s`

**Steps:**
1. Traverse both strings simultaneously.
2. If a mapping already exists, check consistency.
3. If not, create new mapping in both directions.
4. If any conflict arises, return false.
5. After traversal, return true.

---

## ⏱ Complexity

- **Time Complexity:** O(n), where n = length of strings.
- **Space Complexity:** O(1), since at most 256 ASCII characters.

---

## ✅ Java Code

```java
import java.util.*;

class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) return false;
        
        Map<Character, Character> mapST = new HashMap<>();
        Map<Character, Character> mapTS = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char c1 = s.charAt(i);
            char c2 = t.charAt(i);
            
            // Check s → t mapping
            if (mapST.containsKey(c1)) {
                if (mapST.get(c1) != c2) return false;
            } else {
                mapST.put(c1, c2);
            }
            
            // Check t → s mapping
            if (mapTS.containsKey(c2)) {
                if (mapTS.get(c2) != c1) return false;
            } else {
                mapTS.put(c2, c1);
            }
        }
        
        return true;
    }
}
```
