# LeetCode 380 – Insert Delete GetRandom O(1)

## Problem Understanding

We need to design a `RandomizedSet` class that supports three operations in average O(1) time:

- `insert(val)`: Inserts an element if not already present. Returns `true` if inserted, `false` otherwise.
- `remove(val)`: Removes an element if present. Returns `true` if removed, `false` otherwise.
- `getRandom()`: Returns a random element from the current set with equal probability for each element.

**The main challenge:** Achieving O(1) for all three operations.

- A normal list gives O(1) insertion and random access, but removal is O(n).
- A HashSet gives O(1) insertion and deletion, but random access is O(n).
- **We need a hybrid approach.**

---

## Example

**Operations:**  
`["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]`  
**Arguments:**  
`[[], [1], [2], [2], [], [1], [2], []]`

**Step-by-step:**
1. `insert(1)` → true, set = [1]
2. `remove(2)` → false, set = [1]
3. `insert(2)` → true, set = [1, 2]
4. `getRandom()` → returns 1 or 2
5. `remove(1)` → true, set = [2]
6. `insert(2)` → false (already exists), set = [2]
7. `getRandom()` → returns 2

---

## Key Insight

- Use a **HashMap** to store value → index mapping for O(1) insert and remove checks.
- Use an **ArrayList** to store actual values for O(1) random access.
- **Trick for O(1) removal:**  
  When removing an element, swap it with the last element in the list, update its index in the map, then remove the last element.

---

## Optimal Algorithm

**Steps:**

- **insert(val):**
  - If val exists in map, return false.
  - Else, add it to the end of list and store val → index in map. Return true.
- **remove(val):**
  - If val not in map, return false.
  - Else, get its index, swap it with last element in list, update the map for swapped element, remove last element, delete val from map. Return true.
- **getRandom():**
  - Return a random element from list using Random.

---

⏳ **Time Complexity:** O(1) average for all operations.  
💾 **Space Complexity:** O(n) for list + map.

---

## Java Code

```java
import java.util.*;

class RandomizedSet {
    private List<Integer> list;
    private Map<Integer, Integer> map;
    private Random rand;

    public RandomizedSet() {
        list = new ArrayList<>();
        map = new HashMap<>();
        rand = new Random();
    }

    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        map.put(val, list.size());
        list.add(val);
        return true;
    }

    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        int idx = map.get(val);
        int lastElement = list.get(list.size() - 1);

        // Swap with last element
        list.set(idx, lastElement);
        map.put(lastElement, idx);

        // Remove last element
        list.remove(list.size() - 1);
        map.remove(val);
        return true;
    }

    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}
```

---

## Dry Run

**Input:**  
`["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]`  
`[[], [1], [2], [2], [], [1], [2], []]`

- `insert(1)` → list = [1], map = {1:0}, returns true
- `remove(2)` → not found, returns false
- `insert(2)` → list = [1,2], map = {1:0, 2:1}, returns true
- `getRandom()` → returns 1 or 2
- `remove(1)` → swap with last element → list = [2], map = {2:0}, returns true
- `insert(2)` → already exists, returns false
- `getRandom()` → returns 2

✅ **Output:** `[null, true, false, true, 2, true, false, 2]`
