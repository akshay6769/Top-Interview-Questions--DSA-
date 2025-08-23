# LeetCode 68 – Text Justification

## 🔍 Problem Understanding

We need to format text so that:
- Each line has exactly `maxWidth` characters.
- Words are greedily packed into each line.
- Extra spaces must be distributed evenly between words.
- If spaces don’t divide evenly, the left slots get more spaces.
- The last line must be left-aligned (normal spaces, no justification).

---

## 🧠 Thought Process / Approach

### Greedy Packing of Words
- Start from the first word, keep adding words until adding another would exceed `maxWidth`.
- That group of words forms a line.

### Handle Three Cases
1. **Last line:** Left justify → words separated by single spaces, pad remaining spaces at the end.
2. **Single word line:** Left justify → word followed by trailing spaces.
3. **Normal line:**  
   - Calculate total spaces = `maxWidth - totalCharsOfWords`.
   - Distribute spaces evenly between words.
   - If spaces don’t divide evenly, left gaps get more spaces.

Continue until all words are processed.

---

## ⚡ Complexity

- **Time Complexity:** O(N) (every word is processed once, plus space distribution)
- **Space Complexity:** O(1) (ignoring output storage)

---

## ✅ Optimal Java Code

```java
import java.util.*;

class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> result = new ArrayList<>();
        int index = 0;

        while (index < words.length) {
            int totalChars = words[index].length();
            int last = index + 1;

            // Find how many words can fit in this line
            while (last < words.length) {
                if (totalChars + 1 + words[last].length() > maxWidth) break;
                totalChars += 1 + words[last].length();
                last++;
            }

            StringBuilder line = new StringBuilder();
            int numOfWords = last - index;

            // Case 1: Last line OR single word
            if (last == words.length || numOfWords == 1) {
                for (int i = index; i < last; i++) {
                    line.append(words[i]).append(" ");
                }
                line.deleteCharAt(line.length() - 1); // remove trailing space
                while (line.length() < maxWidth) line.append(" ");
            } else {
                // Case 2: Fully justified
                int spaces = (maxWidth - totalChars + (numOfWords - 1)) / (numOfWords - 1);
                int extraSpaces = (maxWidth - totalChars + (numOfWords - 1)) % (numOfWords - 1);

                for (int i = index; i < last - 1; i++) {
                    line.append(words[i]);
                    for (int s = 0; s < spaces; s++) line.append(" ");
                    if (extraSpaces-- > 0) line.append(" ");
                }
                line.append(words[last - 1]); // last word in line
            }

            result.add(line.toString());
            index = last;
        }
        return result;
    }
}
```

---

✅ This algorithm is optimal and runs in O(N) where N = total characters in words.  
💡 It carefully handles last line, single word lines, and full justification.
