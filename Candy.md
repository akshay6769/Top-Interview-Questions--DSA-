# LeetCode 135 – Candy

## Problem Understanding

We have `n` children standing in a line, each with a rating. We need to give them candies with two rules:

- Every child gets at least one candy.
- Children with higher ratings than their immediate neighbors get more candies.

**Goal:** Minimize the total number of candies distributed.

---

## Key Observations

- If ratings increase from left to right, the candies should increase accordingly.
- If ratings decrease from right to left, we must also increase candies accordingly.
- A single pass from left to right is not enough — a high rating on the left might not be handled unless we also check from right to left.
- We need **two passes**:
  - Left → Right pass ensures rule #2 for increasing ratings.
  - Right → Left pass ensures rule #2 for decreasing ratings.

---

## Optimal Algorithm

1. Initialize an array `candies` of length `n` with all values = 1 (minimum candies).
2. **First pass (Left to Right):**
   - If `ratings[i] > ratings[i-1]`, set `candies[i] = candies[i-1] + 1`.
3. **Second pass (Right to Left):**
   - If `ratings[i-1] > ratings[i]`, set `candies[i-1] = max(candies[i-1], candies[i] + 1)`.
4. Sum up all candies to get the answer.

---

## Complexity Analysis

- **Time Complexity:** O(n) — two passes over the array.
- **Space Complexity:** O(n) — for the candies array.

---

## Java Code

```java
import java.util.Arrays;

class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length;
        int[] candies = new int[n];
        Arrays.fill(candies, 1);
        
        // Step-1: Left to Right
        for (int i = 1; i < n; ++i) {
            if (ratings[i] > ratings[i-1]) {
                candies[i] = 1 + candies[i-1];
            }
        }
        
        // Step-2: Right to Left
        int total = candies[n-1];
        for (int i = n-1; i > 0; --i) {
            if (ratings[i-1] > ratings[i]) {
                candies[i-1] = Math.max(candies[i-1], 1 + candies[i]);
            }
            total += candies[i-1];
        }
        
        return total;
    }
}
```
