# Best Time to Buy and Sell Stock — LeetCode #121

## Problem Link
[LeetCode: Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## Problem Statement (Simplified)
You are given an array `prices` where `prices[i]` represents the price of a given stock on the `i-th` day.

Your task is to maximize your profit by choosing a single day to buy one stock and a different day in the future to sell that stock.

Return the maximum profit you can achieve. If no profit is possible, return 0.

---

## Constraints
- 1 <= prices.length <= 10^5
- 0 <= prices[i] <= 10^4

---

## Submitted Solutions

### Submission 1 & 2: Greedy Approach Using Conditional Checks

```java
class Solution {
    public int maxProfit(int[] prices) {
        int buy = prices[0];
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < buy) {
                buy = prices[i];
            } else if (prices[i] - buy > profit) {
                profit = prices[i] - buy;
            }
        }
        return profit;
    }
}
```

### Approach
- Start by assuming the first day as the minimum buy price.
- Iterate through the array while tracking:
  - The lowest price so far to buy
  - The highest profit you can make at each day if you sell at that price
- Update `profit` only when a better sell opportunity is found.

### Time and Space Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

---

### Submission 3: Max/Min Consolidated Update Pattern

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int mini = prices[0];

        for (int i = 1; i < prices.length; i++) {
            int currProfit = prices[i] - mini;
            maxProfit = Math.max(maxProfit, currProfit);
            mini = Math.min(mini, prices[i]);
        }
        return maxProfit;
    }
}
```

### Approach
- Tracks `mini` as the minimum price seen so far.
- At each iteration:
  - Calculate `currProfit = prices[i] - mini`
  - Update `maxProfit` if the current profit is better
  - Update `mini` for future iterations

### Comparison
- Functionally identical to the first approach
- More compact and idiomatic using `Math.max()` and `Math.min()`

---

## Key Concepts Utilized
- Greedy algorithm for optimal transaction timing
- One-pass solution with constant space
- Difference tracking between current price and historical minimum

---

## Edge Cases Considered
- Strictly decreasing prices: Output should be 0 (no profit possible)
- Only one price in array: Not enough data to complete a transaction
- Large spikes or dips in price: Ensures the algorithm still identifies correct min and max days

---

## Clarifications and Follow-ups Asked
- Can this be extended to allow multiple transactions?
- Can we solve this using Dynamic Programming?
- What are the parallels between this and Kadane’s Algorithm?

---

## Final Thoughts
The greedy approach with a single traversal is optimal for this version of the problem. It ensures minimal runtime and memory usage, making it ideal for large inputs. This problem also helps build foundational thinking for problems involving local minima and maxima in an array context.
