# ✅ LeetCode 169: Majority Element

## 📝 Problem Explanation

You're given an integer array `nums` of size `n`.

**Majority element:** The element that appears more than ⌊n/2⌋ times.  
It's guaranteed that the majority element always exists.

---

## 🎯 Goals

- Find and return the majority element.
- Solve in O(n) time (linear scan) and O(1) extra space (constant memory).

---

## 🧠 Optimal Algorithm: Boyer-Moore Voting Algorithm

This algorithm works by canceling out pairs of different elements, leaving the majority element as the final candidate because it appears more than half the time.

### 🔄 Algorithm Steps

1. **Initialize:**
    - `candidate = 0`
    - `count = 0`
2. **Traverse the array:**
    - If `count == 0`, set `candidate = num`.
    - If `num == candidate`, increment `count`.
    - Else, decrement `count`.
3. **After the loop, `candidate` will be the majority element.**

---

## ⏱ Time Complexity

- O(n): Single pass through the array.

## 📦 Space Complexity

- O(1): No extra data structures used.

---

## ✅ Java Code

```java
public class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        int candidate = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```

---

## 🧪 Example Walkthrough

**Input:**  
`nums = [2, 2, 1, 1, 1, 2, 2]`

**Process:**

- Start: `candidate = 0`, `count = 0`
- See 2: `count == 0` → `candidate = 2`, `count = 1`
- See 2: `candidate = 2` → `count = 2`
- See 1: `candidate != 1` → `count = 1`
- See 1: `candidate != 1` → `count = 0`
- See 1: `count == 0` → `candidate = 1`, `count = 1`
- See 2: `candidate != 2` → `count = 0`
- See 2: `count == 0` → `candidate = 2`, `count = 1`

**Final Output:**  
`majorityElement = 2`
