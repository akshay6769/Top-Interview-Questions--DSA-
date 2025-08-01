# ✅ LeetCode 80: Remove Duplicates from Sorted Array II

## 📝 Problem Explanation

You're given a sorted integer array `nums` (non-decreasing order).

**Task:**  
Remove duplicates in-place such that each unique element appears at most twice.

- Modify the array in-place to keep at most two occurrences of each element.
- Return `k`, the number of elements in the modified array.
- Use O(1) extra space (in-place).

---

## 🧠 Optimal Algorithm: Two-Pointer Approach

This is an advanced version of the original “Remove Duplicates” problem, where we allow up to 2 occurrences of each element.

### 🔄 Algorithm Steps

1. Use an index `i` to track the position of the next write.
2. Loop through the array with `j` (read pointer).
3. If `i < 2` → always write `nums[j]`.
4. If `nums[j] != nums[i - 2]` → write it (i.e., it's not a third+ duplicate).
5. Else, skip (ignore the extra duplicate).

---

## ⏱ Time & 📦 Space Complexity

- **Time Complexity:** O(n) – one pass through the array.
- **Space Complexity:** O(1) – in-place, no extra data structures.

---

## ✅ Java Code

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 2) return nums.length;

        int i = 2; // start from index 2, since first two elements are always allowed
        for (int j = 2; j < nums.length; j++) {
            if (nums[j] != nums[i - 2]) {
                nums[i] = nums[j];
                i++;
            }
        }
        return i; // length of final array
    }
}
```

---

## 🧪 Example Walkthrough

**Input:**  
`nums = [1,1,1,2,2,3]`

**Output:**  
`k = 5`  
`nums = [1,1,2,2,3,_]`

**Explanation:**
- First two 1s → keep
- Third 1 → skip
- First two 2s → keep
- 3 → keep
