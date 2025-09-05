# LeetCode 30 – Substring with Concatenation of All Words

## 🔎 Problem Understanding

Given:
- A string `s`.
- An array of words `words`, where all words have the same length.

**Find all starting indices in `s` where a substring is formed by concatenating all words in `words` exactly once and without any extra characters.**

### Example:
```
s = "barfoothefoobarman", words = ["foo", "bar"]

Substring "barfoo" at index 0 ✅
Substring "foobar" at index 9 ✅
Answer → [0, 9]
```

---

## 🛠️ Optimal Approach (Sliding Window + HashMap)

### Preprocessing
- Store word frequencies in a HashMap `wordCount`.

### Sliding Window
- Each word has the same length = `wordLen`.
- Total window size = `wordLen * words.length`.

### Iterate with offset
- Start from indices `0 → wordLen-1` (to handle alignment with word boundaries).
- Move a sliding window, extracting substrings of size `wordLen`.
- Maintain a `seenWords` map to track frequencies.

### Check validity
- If a word is not in `wordCount`, reset the window.
- If word appears too many times, shrink window from the left.
- If all words matched → record starting index.

---

## ⏱️ Complexity

- **Time Complexity:** O(n × wordLen), where n = length of s.
- **Space Complexity:** O(k), where k = number of unique words.

---

## ✅ Java Code

```java
import java.util.*;

class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> result = new ArrayList<>();
        if (s == null || words == null || words.length == 0) return result;

        int wordLen = words[0].length();
        int wordCount = words.length;
        int totalLen = wordLen * wordCount;

        if (s.length() < totalLen) return result;

        // Step 1: Build frequency map of words
        Map<String, Integer> wordMap = new HashMap<>();
        for (String w : words) {
            wordMap.put(w, wordMap.getOrDefault(w, 0) + 1);
        }

        // Step 2: Sliding window with offsets
        for (int i = 0; i < wordLen; i++) {
            int left = i, right = i;
            Map<String, Integer> seen = new HashMap<>();
            int count = 0;

            while (right + wordLen <= s.length()) {
                String word = s.substring(right, right + wordLen);
                right += wordLen;

                if (wordMap.containsKey(word)) {
                    seen.put(word, seen.getOrDefault(word, 0) + 1);
                    count++;

                    // If word seen too many times, shrink window
                    while (seen.get(word) > wordMap.get(word)) {
                        String leftWord = s.substring(left, left + wordLen);
                        seen.put(leftWord, seen.get(leftWord) - 1);
                        left += wordLen;
                        count--;
                    }

                    // If all words matched → record start index
                    if (count == wordCount) {
                        result.add(left);
                    }
                } else {
                    // Reset if invalid word
                    seen.clear();
                    count = 0;
                    left = right;
                }
            }
        }

        return result;
    }
}
```

---

✅ This solution efficiently handles large strings (`s.length ≤ 10^4`) and multiple words (`words.length ≤ 5000`).  
✅ Uses sliding window + HashMap for optimal performance.
