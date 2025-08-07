# 🔹 LeetCode 45 – Jump Game II

## 🧠 Problem Summary

You're given an array `nums`, where each element `nums[i]` indicates the maximum jump length you can make from that position.

- You start at index 0.
- Your goal is to reach the last index in the minimum number of jumps.
- It is guaranteed that the last index is reachable.

---

## ✅ Example

**Input:**  
`nums = [2,3,1,1,4]`  
**Output:** `2`

**Explanation:**  
- Jump 1 → from index 0 to index 1 (jump length = 1)  
- Jump 2 → from index 1 to index 4 (jump length = 3)

---

## 🛠️ Optimal Approach: Greedy

Use a greedy traversal, tracking:
- `farthest`: The farthest index we can currently reach.
- `end`: The end of the current jump window.
- `jumps`: Count of jumps made.

**At every index:**
1. Update the farthest index reachable so far.
2. If we reach the end of our current jump window, we make a jump and update `end` to `farthest`.

---

## ⏱️ Time Complexity

- O(n)

## 📦 Space Complexity

- O(1)

---

## ✅ Java Code

```java
class Solution {
    public int jump(int[] nums) {
        int jumps = 0;
        int farthest = 0;
        int end = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            farthest = Math.max(farthest, i + nums[i]);

            if (i == end) {
                jumps++;
                end = farthest;
            }
        }

        return jumps;
    }
}
```
