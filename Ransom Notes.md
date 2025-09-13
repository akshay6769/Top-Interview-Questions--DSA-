# LeetCode 383 – Ransom Note

## 🔎 Problem Recap

We need to check if `ransomNote` can be constructed from `magazine` where:
- Each character from magazine can be used **only once**.
- Return `true` if possible, else `false`.

---

## ⚡ Algorithm (Using HashMap)

1. **Build Character Frequency Map**  
   Create a `HashMap<Character, Integer>` to store the frequency of each character in `magazine`.
   - **Key:** character
   - **Value:** count of occurrences

2. **Traverse the ransomNote**  
   For each character `c`:
   - Check if it exists in the map and has a positive count.
   - If not found or count is 0, return `false`.
   - Otherwise, decrement the count in the map.

3. **Return true**  
   If we finish the loop successfully, all required characters are available.

---

## ⏱️ Complexity

- **Time Complexity:** O(m + n) →  
  `m` = length of `ransomNote`, `n` = length of `magazine`.
- **Space Complexity:** O(k),  
  `k` = distinct characters (≤ 26 for lowercase letters).

---

## 💻 Java Code (HashMap Approach)

```java
import java.util.*;

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character, Integer> map = new HashMap<>();
        
        // Count characters in magazine
        for (char c : magazine.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        
        // Check ransomNote characters
        for (char c : ransomNote.toCharArray()) {
            if (!map.containsKey(c) || map.get(c) == 0) {
                return false; // not enough characters
            }
            map.put(c, map.get(c) - 1); // use one occurrence
        }
        
        return true;
    }
}
```

---

## ✅ Notes

- The array approach is faster and optimal since we only have lowercase letters.
- The HashMap approach is more general and works for **any character set**.
