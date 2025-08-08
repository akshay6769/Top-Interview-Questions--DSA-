# 🔹 LeetCode 274 – H-Index

## 🧠 Problem Summary

Given an array `citations` where `citations[i]` is the number of citations for the i-th paper, return the H-index of the researcher.

The H-index is the maximum `h` such that the researcher has at least `h` papers with ≥ `h` citations each.

---

## ✅ Example

**Input:**  
`citations = [3,0,6,1,5]`

**Output:**  
`3`

**Explanation:**  
We have 3 papers with at least 3 citations each:  
`[6, 5, 3]` → satisfies h = 3.

---

## 🛠️ Optimal Approach: Sorting + Linear Scan

Steps:
1. Sort the array in ascending order.
2. For each paper at index `i`, calculate how many papers have at least `citations[i]` citations → `n - i`.
3. The first time `citations[i] >= n - i`, that value is the H-index.

---

## ⏱️ Time Complexity

- O(n log n) (sorting)

## 📦 Space Complexity

- O(1) (in-place sort)

---

## ✅ Java Code

```java
import java.util.Arrays;

class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length;
        
        for (int i = 0; i < n; i++) {
            int papersWithAtLeastThis = n - i;
            if (citations[i] >= papersWithAtLeastThis) {
                return papersWithAtLeastThis;
            }
        }
        return 0;
    }
}
```
