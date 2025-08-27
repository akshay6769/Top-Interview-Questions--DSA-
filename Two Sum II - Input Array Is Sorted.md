# LeetCode 167 – Two Sum II: Input Array Is Sorted

## 🔎 Problem Restatement

Given a **sorted array** `numbers` (1-indexed) and a target integer, return the indices `[i, j]` such that:

- `numbers[i] + numbers[j] == target`
- `1 <= i < j <= numbers.length`
- There’s **exactly one solution**
- Must use **O(1) extra space**

---

## ⚡ Optimal Algorithm (Two Pointers)

Because the array is sorted in non-decreasing order, we use the **two-pointer technique**:

- Start with two pointers:
  - `start = 0` (first element)
  - `end = n-1` (last element)
- Compute the sum:
  - If `sum == target` → return `[start+1, end+1]`
  - If `sum > target` → move `end--` to reduce the sum
  - If `sum < target` → move `start++` to increase the sum
- Repeat until the pair is found

**Why this works:**  
As the array is sorted, moving pointers always takes us closer to the target.

---

## ⏱️ Time & Space Complexity

- **Time Complexity:** O(n) (single pass over the array)
- **Space Complexity:** O(1) (only pointers used)

---

## ✅ Explanation of Your Code

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length;
        int start = 0;       // left pointer
        int end = n - 1;     // right pointer

        while (start < end) {
            int sum = numbers[start] + numbers[end];

            if (sum == target) {
                return new int[] {start + 1, end + 1}; // return 1-indexed result
            }
            else if (sum > target) {
                end--;  // move right pointer left to reduce sum
            }
            else {
                start++; // move left pointer right to increase sum
            }
        }
        return new int[] {-1, -1}; // shouldn't happen as problem guarantees one solution
    }
}
```
