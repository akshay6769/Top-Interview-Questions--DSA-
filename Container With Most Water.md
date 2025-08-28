# LeetCode 11 – Container With Most Water

## 🔎 Problem Understanding

We are given an array `height[]` where each element represents the height of a vertical line.

**Task:**  
Select two lines such that the container formed between them (with the x-axis as the base) can hold the **maximum water**.

The area between two lines is determined by:

```
Area = min(height[left], height[right]) × (right − left)
```

*Why min?*  
Water can only be stored up to the shorter line’s height.

---

## 🛠️ Naive Approach (Brute Force)
- Try all pairs `(i, j)` → calculate area.
- Keep track of the maximum area.
- **Time Complexity:** O(n²) → too slow for n = 10^5.

---

## ✅ Optimal Approach (Two Pointers)

Use two pointers (`left` at start, `right` at end):

1. Compute the area with current `left` and `right`.
2. Update `maxArea`.
3. Move the pointer with the smaller height inward (only moving the shorter line can potentially increase area):
   - If `height[left] < height[right]`, do `left++`.
   - Else, do `right--`.
4. Repeat until `left < right`.

---

## 📊 Complexity Analysis

- **Time Complexity:** O(n) → each element visited at most once.
- **Space Complexity:** O(1).

---

## 💻 Java Code (Two Pointers Solution)

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int maxArea = 0;

        while (left < right) {
            // Calculate current area
            int width = right - left;
            int minHeight = Math.min(height[left], height[right]);
            int area = width * minHeight;

            // Update maximum area found so far
            maxArea = Math.max(maxArea, area);

            // Move the smaller line inward
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;
    }
}
```

---

## 👉 Key Intuition

Even though we lose some possibilities by moving one pointer, moving the taller line inward can **never increase area**, so the optimal strategy is always to move the shorter line.
