# ✅ LeetCode 55: Jump Game

## 📝 Problem Explanation

You are given an array `nums`, where each element `nums[i]` represents the maximum jump length you can make from that index.  
Starting at index 0, determine if you can reach the last index.

---

## 🎯 Goals

- Return `true` if the last index is reachable, otherwise `false`.
- Solve efficiently in linear time.

---

## 🧠 Optimal Algorithm: Greedy Approach

Track the farthest index you can reach while traversing the array:

1. Initialize `maxLen = 0` (stores the maximum reachable index so far).
2. Iterate through the array:
   - If the current index `i` is greater than `maxLen`, you cannot move further → return `false`.
   - Otherwise, update `maxLen = max(maxLen, i + nums[i])`.
3. After the loop, if you never got stuck, return `true`.

---

## ⏱ Time Complexity

- O(n) – Single pass through the array.

## 📦 Space Complexity

- O(1) – No extra data structures.

---

## 💻 Java Code

```java
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int maxLen = 0;
        for (int i = 0; i < n; i++) {
            if (i > maxLen) return false;
            maxLen = Math.max(maxLen, i + nums[i]);
        }
        return true;
    }
}
```

---

## 🧪 Example Walkthrough

**Input:** `nums = [2,3,1,1,4]`
- Start: `maxLen = 0`
- i=0 → `maxLen = max(0, 0+2) = 2`
- i=1 → `maxLen = max(2, 1+3) = 4` → Can reach last index → return `true`

**Input:** `nums = [3,2,1,0,4]`
- i=0 → `maxLen = 3`
- i=1 → `maxLen = 3`
- i=2 → `maxLen = 3`
- i=3 → `maxLen = 3`
- i=4 → stuck because `4 > maxLen` → return `false`
