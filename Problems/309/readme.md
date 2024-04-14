# [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

- After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

**Example 1:**

**Input:** prices = [1,2,3,0,2]
**Output:** 3
**Explanation:** transactions = [buy, sell, cooldown, buy, sell]

**Example 2:**

**Input:** prices = [1]
**Output:** 0

## **Constraints:**

- `1 <= prices.length <= 5000`
- `0 <= prices[i] <= 1000`

## Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0

        n = len(prices)
        hold, sold, rest = [0]*n, [0]*n, [0]*n

        hold[0] = -prices[0]
        sold[0] = 0
        rest[0] = 0

        for i in range(1, n):
            hold[i] = max(hold[i-1], rest[i-1] - prices[i])
            sold[i] = hold[i-1] + prices[i]
            rest[i] = max(rest[i-1], sold[i-1])

        return max(sold[n-1], rest[n-1])


```

## Thoughts

### Time Complexity

O(n): We iterate through the list prices once, performing constant-time operations for each day.

### Space Complexity

O(n): We use three additional arrays, hold, sold, and rest, each of size n.

## Space optimized O(1) space

We can optimize the space complexity to O(1) by keeping only the last values of hold, sold, and rest instead of the entire arrays.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices:
            return 0

        hold = -prices[0]
        sold = 0
        rest = 0

        for price in prices[1:]:
            prev_hold = hold
            hold = max(hold, rest - price)
            rest = max(rest, sold)
            sold = prev_hold + price

        return max(sold, rest)
```
