# LeetCode 15 – 3Sum

## 🔎 Problem Recap

Find all **unique triplets** `(nums[i], nums[j], nums[k])` in an array such that:

```
nums[i] + nums[j] + nums[k] = 0
```

**Constraints:**
- No duplicate triplets allowed.
- Order of triplets doesn’t matter.

---

## ⚡ Naive Approach (Brute Force)

- Check all triplets `(i, j, k)` → O(n³).
- Too slow for n = 3000.

---

## ✅ Optimal Approach: Sorting + Two Pointers

Reduce to O(n²) using sorting and the two-pointer technique.

**Steps:**
1. Sort the array → helps manage duplicates and use two-pointer search.
2. Fix one element (`nums[i]`) as the first element of triplet.
3. Use two pointers (`left`, `right`) to find the other two numbers:
   - If `nums[i] + nums[left] + nums[right] == 0` → store triplet.
   - If sum < 0 → move `left++` (to increase sum).
   - If sum > 0 → move `right--` (to decrease sum).
   - Skip duplicates for `i`, `left`, and `right`.

---

## ⏱️ Complexity

- **Time Complexity:** O(n²) (outer loop O(n) × two-pointer O(n))
- **Space Complexity:** O(1) (ignoring output list)

---

## 💻 Java Code (Optimal Solution)

```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Step 1: sort

        for (int i = 0; i < nums.length - 2; i++) {
            // Skip duplicate 'i'
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1, right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));

                    // Skip duplicate 'left' and 'right'
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;

                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;  // Need larger sum
                } else {
                    right--; // Need smaller sum
                }
            }
        }
        return result;
    }
}
```

---

✅ This solution efficiently handles duplicates and guarantees all unique triplets.
