# ✅ LeetCode 27: Remove Element

## 🔍 Problem Summary

You're given an integer array `nums` and an integer `val`.

**Task:** Remove all instances of `val` in-place and return the new length `k`.  
The first `k` elements of `nums` should contain the elements that are not equal to `val`.  
The order of elements can be changed, and you don't need to care about elements beyond the new length.

---

## 📘 Example

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
```

---

## ⚙️ Algorithm (Optimal – In-Place)

### 💡 Key Idea:
Use two pointers:
- One (`i`) iterates through the array.
- One (`k`) keeps track of where to place the next non-`val` element.

### 🔁 Steps:

1. Initialize `k = 0`
2. Traverse the array:
    - If `nums[i] != val`, assign `nums[k] = nums[i]` and increment `k`
3. After the loop, `k` will be the new length of the array.

---

## ✅ Java Code (Clean Version)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int k = 0; // New length
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
}
```

---

## 🧠 Dry Run

Input: `nums = [0,1,2,2,3,0,4,2]`, `val = 2`

Initial: `k = 0`

| i | nums[i] | Action              | nums array after | k |
|---|---------|---------------------|------------------|---|
| 0 |   0     | keep (nums[0]=0)    | [0,1,2,2,3,0,4,2]| 1 |
| 1 |   1     | keep (nums[1]=1)    | [0,1,2,2,3,0,4,2]| 2 |
| 2 |   2     | skip                |                  | 2 |
| 3 |   2     | skip                |                  | 2 |
| 4 |   3     | keep (nums[2]=3)    | [0,1,3,2,3,0,4,2]| 3 |
| 5 |   0     | keep (nums[3]=0)    | [0,1,3,0,3,0,4,2]| 4 |
| 6 |   4     | keep (nums[4]=4)    | [0,1,3,0,4,0,4,2]| 5 |
| 7 |   2     | skip                |                  | 5 |

Result: `[0,1,3,0,4,...]`, `k = 5`

---

## 📊 Time & Space Complexity

- **Time Complexity:** O(n) – single pass
- **Space Complexity:** O(1) – in-place
