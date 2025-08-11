# LeetCode 134 – Gas Station

## 📌 Key Observations

### Total Gas vs Total Cost
- If `sum(gas) < sum(cost)`, it’s impossible to complete the loop. Return -1 immediately.

### Finding the Start Point
- Scan once through the stations:
  - Keep track of current fuel in tank.
  - If current fuel < 0, we cannot reach this station from the current start point — so choose the next station as the new start and reset fuel.

### Uniqueness Guarantee
- Problem states the solution is unique, so if total gas ≥ total cost, there’s exactly one valid start.

---

## 🛠 Optimal Algorithm (Greedy Approach)
**Steps:**
1. Compute total gas and total cost. If `totalGas < totalCost` → return -1.
2. Initialize:  
   `start = 0`  
   `tank = 0`
3. Loop through each station:
   - Add `gas[i] - cost[i]` to tank.
   - If `tank < 0`, set:
     - `start = i + 1`
     - Reset `tank = 0`
4. Return `start` as the answer.

---

⏱ **Time Complexity:** O(n) (single pass)  
📦 **Space Complexity:** O(1) (only variables)

---

## 💻 Java Code

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0, totalCost = 0;
        int tank = 0, start = 0;

        for (int i = 0; i < gas.length; i++) {
            totalGas += gas[i];
            totalCost += cost[i];
            tank += gas[i] - cost[i];

            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }

        return totalGas < totalCost ? -1 : start;
    }
}
```
