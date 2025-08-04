# ✅ LeetCode 121: Best Time to Buy and Sell Stock

## 📝 Problem Explanation

You are given an array `prices`, where:
- `prices[i]` = price of a stock on the i-th day.
- You must buy on one day and sell on a later day.

**Goal:**  
Maximize profit = sell_price - buy_price.  
If no profit is possible, return 0.

---

## 🧠 Optimal Algorithm: Single Pass (Greedy Approach)

The problem boils down to finding:
- Minimum price so far (best day to buy).
- Maximum profit achievable on each day.

---

### 🔄 Algorithm Steps

1. **Initialize:**
    - `minPrice = Integer.MAX_VALUE` (to track lowest buy price)
    - `maxProfit = 0` (to track maximum profit)
2. **Iterate through the prices array:**
    - Update `minPrice` if current price is lower.
    - Calculate potential profit: `prices[i] - minPrice`.
    - Update `maxProfit` if potential profit is higher.
3. **Return `maxProfit`.**

---

## ⏱ Time Complexity

- O(n): Single pass through the array.

## 📦 Space Complexity

- O(1): No extra space used.

---

## 💻 Java Code

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int price : prices) {
            if (price < minPrice) {
                minPrice = price; // update lowest price
            } else if (price - minPrice > maxProfit) {
                maxProfit = price - minPrice; // update maximum profit
            }
        }

        return maxProfit;
    }
}
```

---

## 🧪 Example Walkthrough

**Input:**  
`prices = [7,1,5,3,6,4]`

**Steps:**
- Day 1: `minPrice = 7`, `maxProfit = 0`
- Day 2: `minPrice = 1`, `maxProfit = 0`
- Day 3: potential profit = `5-1 = 4` → `maxProfit = 4`
- Day 4: potential profit = `3-1 = 2` → `maxProfit = 4` (unchanged)
- Day 5: potential profit = `6-1 = 5` → `maxProfit = 5`
- Day 6: potential profit = `4-1 = 3` → `maxProfit = 5` (unchanged)

**Output:**  
Max Profit = 5
