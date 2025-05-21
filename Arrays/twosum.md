#  Two Sum — LeetCode #1

## 🔗 Problem Link
[LeetCode: Two Sum](https://leetcode.com/problems/two-sum/)

##  Problem Statement (Simplified)
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the target.

- Each input will have exactly one solution.
- You may not use the same element twice.
- Return the answer in any order.

---

##  Constraints
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`

---

##  Approaches I Used

### 1️ Brute Force — O(n²)

#### Method:
Nested loops to check all possible pairs.

```java
for (int i = 0; i < nums.length; i++) {
    for (int j = i + 1; j < nums.length; j++) {
        if (nums[i] + nums[j] == target) {
            return new int[]{i, j};
        }
    }
}
```

#### Analysis:
- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)
-  Easy to implement, but inefficient for large inputs.

---

### 2️ Optimized using HashMap — O(n)

#### Method:
- Store elements in a `HashMap<value, index>`.
- For each element `x`, check if `target - x` exists in the map.

```java
Map<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < nums.length; i++) {
    int complement = target - nums[i];
    if (map.containsKey(complement)) {
        return new int[]{map.get(complement), i};
    }
    map.put(nums[i], i);
}
```

#### Analysis:
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)
-  Highly efficient. Great trade-off between speed and memory.

---

##  Key Methods Used
- `HashMap.containsKey()`: For constant-time lookups.
- Hash-based indexing to avoid nested loops.
- Integer math & early return for performance.

---

##  Edge Cases Considered
- Duplicates in input (e.g., `[3, 3]`, `target = 6`)
- Negative numbers and zero
- Only two elements

---

##  Final Thoughts
- Brute-force is great for understanding, but not scalable.
- HashMap method is clean, readable, and performant.
- This problem teaches **hash-based searching**—essential for interviews!

