# ✅ LeetCode 189: Rotate Array

## 📝 Problem Explanation

You are given an array `nums` and an integer `k`.  
Rotate the array to the right by `k` steps, where `k` is non-negative.

**Key Points:**
- Rotating by `k` means the last `k` elements move to the front.
- Must be done in-place with O(1) extra space.

---

## 🎯 Goals

- Modify the array in-place.
- Achieve O(n) time complexity.
- Use O(1) extra space.

---

## 🧠 Optimal Algorithm: Reverse Approach

We can solve this using array reversal in three steps:

### 🔄 Algorithm Steps

1. **Normalize `k`**: Since rotating by `n` (array length) results in the same array,
    ```java
    k = k % n
    ```
2. **Reverse the entire array**.  
   Example: `[1,2,3,4,5,6,7]` → `[7,6,5,4,3,2,1]`

3. **Reverse the first `k` elements**.  
   Example: `[7,6,5,4,3,2,1]` → `[5,6,7,4,3,2,1]`

4. **Reverse the remaining `n-k` elements**.  
   Example: `[5,6,7,4,3,2,1]` → `[5,6,7,1,2,3,4]`

---

## ⏱ Time Complexity

- O(n): Each element is reversed at most twice.

## 📦 Space Complexity

- O(1): Reversal is done in-place.

---

## ✅ Java Code

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n; // Normalize k

        // Step 1: Reverse the whole array
        reverse(nums, 0, n - 1);

        // Step 2: Reverse first k elements
        reverse(nums, 0, k - 1);

        // Step 3: Reverse remaining n-k elements
        reverse(nums, k, n - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

---

## 🧪 Example Walkthrough

**Input:**  
`nums = [1,2,3,4,5,6,7], k = 3`

**Process:**  
- Normalize k: `k = 3 % 7 = 3`
- Reverse full array: `[7,6,5,4,3,2,1]`
- Reverse first 3: `[5,6,7,4,3,2,1]`
- Reverse last 4: `[5,6,7,1,2,3,4]`

**Output:**  
`[5,6,7,1,2,3,4]`
