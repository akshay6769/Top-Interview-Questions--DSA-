# ✅ LeetCode 26: Remove Duplicates from Sorted Array

## 📝 Problem Explanation

You're given a sorted array `nums` (in non-decreasing order).

**Task:**  
Remove duplicates in-place so that each element appears only once and the relative order is preserved.

- Modify `nums` so the first `k` elements contain only unique elements in the same order.
- Return `k`, the count of unique elements.
- Use O(1) extra space (in-place).

---

## 🧠 Optimal Algorithm: Two-Pointer Technique

Since the array is sorted, duplicates will be adjacent.

### 🔄 Steps

1. Use two pointers:
    - `i` → slow pointer (last position of the unique values)
    - `j` → fast pointer (to scan the array)

2. Start from the second element (`j = 1`).

3. If `nums[j] != nums[i]`, increment `i`, then update `nums[i] = nums[j]`.

4. At the end, return `i + 1` (count of unique elements).

---

## ⏱️ Time & 📦 Space Complexity

- **Time Complexity:** O(n), where n is the length of the array.
- **Space Complexity:** O(1) (in-place)

---

## ✅ Java Code

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int i = 0; // slow pointer
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j]; // copy unique element forward
            }
        }
        return i + 1; // number of unique elements
    }
}
```

---

## 🧪 Example Walkthrough

**Input:**  
`nums = [0,0,1,1,1,2,2,3,3,4]`

**Process:**  
- `i = 0`, `j` moves ahead comparing `nums[j]` to `nums[i]`.
- When a new unique number is found → increment `i`, copy `nums[j]` to `nums[i]`.

**Final Output:**  
- `k = 5`
- `nums = [0,1,2,3,4,...]` (first 5 elements are the unique ones)
