#Source Code 
/**
 * LeetCode 88: Merge Sorted Array
 * 
 * You are given two sorted arrays:
 *   - nums1 of size m + n, where first m elements are valid and last n are 0 (placeholders).
 *   - nums2 of size n.
 * Goal: Merge nums2 into nums1, in-place, resulting in a single sorted array.
 * 
 * Optimal Algorithm (Two Pointers from End)
 * Time: O(m + n), Space: O(1)
 */
# Merge Sorted Array

- **Goal:** Merge nums2 into nums1, in-place, resulting in a single sorted array.

- **Optimal Algorithm (Two Pointers from End)**

- **Time:** O(m + n), **Space:** O(1)

```java
public class MergeSortedArray {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = m - 1;            // Last valid element in nums1
        int p2 = n - 1;            // Last element in nums2
        int p = m + n - 1;         // Last position in nums1

        // Merge from end to start
        while (p1 >= 0 && p2 >= 0) {
            if (nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1];
                p1--;
            } else {
                nums1[p] = nums2[p2];
                p2--;
            }
            p--;
        }

        // Copy remaining elements from nums2, if any
        while (p2 >= 0) {
            nums1[p] = nums2[p2];
            p2--;
            p--;
        }
    }
}
```
-----------------------------------------------------------------------------------------------------------------------------------------------------
#Documentation (Markdown)
# LeetCode 88: Merge Sorted Array

## Problem Summary

You are given two sorted arrays:
- `nums1` of size `m + n`, where first `m` elements are valid and last `n` are 0 (placeholders).
- `nums2` of size `n`.

**Goal**: Merge `nums2` into `nums1`, in-place, resulting in a single sorted array.

---

## Optimal Algorithm (Two Pointers from End)

- To avoid extra space and achieve `O(m + n)` time:
  - Use three pointers:
    - `p1 = m - 1` → end of real elements in `nums1`
    - `p2 = n - 1` → end of `nums2`
    - `p = m + n - 1` → end of total `nums1` (including spaces)
  - Compare from the back and place the larger number at the end.

### Steps

1. Initialize pointers:
   ```java
   p1 = m - 1;
   p2 = n - 1;
   p = m + n - 1;
   ```
2. While both arrays have elements:
   - Compare `nums1[p1]` and `nums2[p2]`
   - Place the larger at `nums1[p]`
   - Move pointers accordingly
3. If any elements remain in `nums2`, copy them over to `nums1`.
4. No need to handle leftover `nums1` elements—they're already in place.

---

## Example Dry Run

```java
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3
// Start comparing from end:
Compare 3 and 6 → place 6
Compare 3 and 5 → place 5
Compare 3 and 2 → place 3
...
Final: [1,2,2,3,5,6]
```

---

## Complexity Analysis

- **Time:** O(m + n)
- **Space:** O(1) (in-place)

---

## How to Run

1. Compile the Java files:
   ```sh
   javac src/MergeSortedArray.java src/MergeSortedArrayTest.java
   ```
2. Run the test:
   ```sh
   java -cp src MergeSortedArrayTest
   ```

---
