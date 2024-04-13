# [322. Coin Change](https://leetcode.com/problems/coin-change/)

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the fewest number of coins that you need to make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

**Example 1:**

**Input:** coins = [1,2,5], amount = 11
**Output:** 3
**Explanation:** 11 = 5 + 5 + 1

**Example 2:**

**Input:** coins = [2], amount = 3
**Output:** -1

**Example 3:**

**Input:** coins = [1], amount = 0
**Output:** 0

## **Constraints:**

- `1 <= coins.length <= 12`
- `1 <= coins[i] <= 231 - 1`
- `0 <= amount <= 104`

## Solution

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0  # Base case: no coins needed to make amount 0

        # Iterate over each amount
        for j in range(1, amount + 1):
            # Check each coin for this amount
            for coin in coins:
                if j >= coin:
                    dp[j] = min(dp[j], dp[j - coin] + 1)

        return dp[amount] if dp[amount] != float('inf') else -1


```

## Thoughts

### Time Complexity

O(n \* m), where n is the number of different coins and m is the total amount.

### Space Complexity

A dynamic programming table (dp) of size m + 1 is used, where m is the amount. This array is used to store the minimum number of coins needed for each amount from 0 to m. Thus, the space complexity is O(m), as the primary storage cost is the dp array which has an entry for each amount up to m.
