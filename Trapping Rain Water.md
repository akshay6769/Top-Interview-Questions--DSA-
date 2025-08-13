# LeetCode 42 – Trapping Rain Water

## Problem Understanding

We’re given an array `height[]` where:
- Each element represents the height of a bar in a histogram.
- Each bar has width = 1.
- We need to calculate how much rainwater can be trapped between these bars after it rains.

---

## Key Intuition

Rainwater can be trapped at a position only if:
- There is a taller bar to the left.
- There is a taller bar to the right.

The amount of water above a bar =  
`min(max height to the left, max height to the right) - height of current bar`  
(but only if this value is positive).

---

## Optimal Algorithm – Two Pointer Technique

We can solve in O(n) time and O(1) extra space using two pointers.

### Steps

1. Initialize two pointers:
   - `left = 0`
   - `right = n - 1`
2. Maintain:
   - `leftMax` = maximum height seen so far from the left.
   - `rightMax` = maximum height seen so far from the right.
3. While `left < right`:
   - If `height[left] < height[right]`:
     - If `height[left] >= leftMax`, update `leftMax`.
     - Else, add `leftMax - height[left]` to water.
     - Move `left++`.
   - Else:
     - If `height[right] >= rightMax`, update `rightMax`.
     - Else, add `rightMax - height[right]` to water.
     - Move `right--`.

---

## Dry Run Example

**height = [0,1,0,2,1,0,1,3,2,1,2,1]**

- Left side max grows until 3, right side max grows until 3.
- Water collected:
  - At index 2: min(1, 3) - 0 = 1
  - At index 5: min(2, 3) - 0 = 2
- ... total = 6

---

## Complexity

- **Time:** O(n) → Each bar is visited at most once.
- **Space:** O(1) → Only a few variables.

---

## Java Code

```java
class Solution {
    public int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int water = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    water += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    water += rightMax - height[right];
                }
                right--;
            }
        }

        return water;
    }
}
```
