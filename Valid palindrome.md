# LeetCode 125 – Valid Palindrome

## 🔎 Problem Understanding

We need to check if a string is a palindrome after:
- Converting all letters to lowercase.
- Removing all non-alphanumeric characters (punctuation, spaces, symbols).

A palindrome reads the same forward and backward.

---

## 🛠️ Optimal Approach (Two Pointers)

We can solve this in `O(n)` time and `O(1)` extra space using the two-pointer technique:

### ✅ Steps:

1. **Initialize two pointers:**
   - `left = 0` (start of string)
   - `right = s.length() - 1` (end of string)
2. **While `left < right`:**
   - Skip non-alphanumeric characters using `Character.isLetterOrDigit()`.
   - Compare characters at `left` and `right` (ignoring case).
   - If mismatch → return `false`.
3. If the loop completes → return `true`.

---

## ⏱️ Complexity Analysis

- **Time Complexity:** O(n) → Each character checked at most once.
- **Space Complexity:** O(1) → Only pointers used.

---

## 💻 Java Code

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            // Skip non-alphanumeric characters
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            // Compare characters ignoring case
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

---

✅ This solution avoids creating extra strings and works efficiently for long inputs (`s.length` up to 2 * 10^5).
