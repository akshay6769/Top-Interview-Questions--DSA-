 # ✅ LeetCode 122: Best Time to Buy and Sell Stock II

## 📝 Problem Explanation

Unlike LeetCode 121 (where you can only buy and sell once), this problem allows multiple transactions to maximize profit.

**Rules:**
- You can buy and sell as many times as you want.
- You cannot hold more than one stock at a time (must sell before buying again).
- You can buy and sell on the same day.

---

## 🎯 Goal

Maximize the total profit by summing up all possible upward price movements.

---

## 🧠 Optimal Algorithm: Greedy Approach

To maximize profit:
- Buy on every local minimum and sell on every local maximum.
- This is equivalent to adding all positive differences (`prices[i] - prices[i-1]`) whenever `prices[i] > prices[i-1]`.

---

### 🔄 Algorithm Steps

1. Initialize `profit = 0`.
2. Traverse the array from day 1 to day n-1.
3. If `prices[i] > prices[i-1]`, add `(prices[i] - prices[i-1])` to profit.
4. Return `profit` as the maximum achievable profit.

---

## ⏱ Time Complexity

- O(n) – single pass.

## 📦 Space Complexity

- O(1) – constant extra space.

---

## ✅ Java Code

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
}
```

---

## 🧪 Example Walkthrough

**Input:** `[7,1,5,3,6,4]`  
- Buy at 1 → Sell at 5 → Profit = 4  
- Buy at 3 → Sell at 6 → Profit = 3  
- **Total Profit = 7**

**Input:** `[1,2,3,4,5]`  
- Profit = (2-1) + (3-2) + (4-3) + (5-4) = 4

**Input:** `[7,6,4,3,1]`  
- No upward movement → Profit = 0
