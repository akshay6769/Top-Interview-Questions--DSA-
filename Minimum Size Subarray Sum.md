# LeetCode 209 – Minimum Size Subarray Sum

## 🔎 Problem Recap

We are given:
- An array of positive integers `nums`.
- A positive integer `target`.

**Task:**  
Find the minimum length of a contiguous subarray whose sum is **≥ target**.  
If no such subarray exists → return `0`.

---

## 🧠 Intuition

Since all numbers are positive:
- Extending the window to the right increases the sum.
- Shrinking the window from the left decreases the sum.

This is a **sliding window problem** (two pointers).

---

## 🛠️ Approach (Sliding Window – O(n))

**Initialize:**
- Two pointers `i` (start) and `j` (end).
- A running sum `sum = 0`.
- A variable `minL` to track the minimum length (initialized to `n+1`).

**Expand window:**
- Move `j` forward, adding `nums[j]` to `sum`.

**Shrink window when possible:**
- If `sum >= target`, we found a valid subarray.
- Update `minL = min(minL, j - i + 1)`.
- Move `i` forward (shrink from left) while keeping `sum >= target`.

**Repeat until `j` reaches the end.**

**Result:**
- If `minL` was updated → return it.
- Else return `0`.

---

## ✅ Why is this Optimal?

- Each element is added once (when `j` moves) and removed once (when `i` moves).
- Thus, **O(n) time** and **O(1) space**.
- This is optimal because we must at least look at all numbers once.

---

## 💻 Java Code (Optimal Solution)

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int n = nums.length;
        int i = 0, j = 0;
        int sum = 0;
        int minL = n + 1;

        while (j < n) {
            sum += nums[j];

            while (sum >= target) {
                minL = Math.min(minL, j - i + 1);
                sum -= nums[i];
                i++;
            }
            j++;
        }
        return minL == n + 1 ? 0 : minL;
    }
}
```

---

## ⏱️ Complexity Analysis

- **Time Complexity:** O(n) → each element is processed at most twice.
- **Space Complexity:** O(1).

---

## ⚡ Follow-Up (O(n log n) solution):

- Use prefix sums + binary search.
- For each index, check the smallest subarray using binary search on prefix sums.
- **Complexity:** O(n log n).
