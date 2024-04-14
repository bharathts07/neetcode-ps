# [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/)

You are given `n` balloons, indexed from `0` to `n - 1`. Each balloon is painted with a number on it represented by an array `nums`. You are asked to burst all the balloons.

If you burst the `ith` balloon, you will get `nums[i - 1] * nums[i] * nums[i + 1]` coins. If `i - 1` or `i + 1` goes out of bounds of the array, then treat it as if there is a balloon with a `1` painted on it.

Return *the maximum coins you can collect by bursting the balloons wisely*.

**Example 1:**

**Input:** nums = [3,1,5,8]
**Output:** 167
**Explanation:**
nums = [3,1,5,8] --> [3,5,8] --> [3,8] --> [8] --> []
coins = 3*1*5 + 3*5*8 + 1*3*8 + 1*8*1 = 167

**Example 2:**

**Input:** nums = [1,5]
**Output:** 10

## **Constraints:**

- `n == nums.length`
- `1 <= n <= 300`
- `0 <= nums[i] <= 100`

## Solution

```python
# DFS solution
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        # Add 1 at both ends for boundary conditions
        nums = [1] + nums + [1]

        dp = {}

        def dfs(l,r):
            if l>r:
                return 0

            if (l,r) in dp:
                return dp[(l,r)]

            dp[(l,r)] = 0
            for i in range(l,r+1):
                coins = nums[l-1] * nums[i] * nums[r+1]
                coins = coins + (dfs(l,i-1) + dfs(i+1,r))
                dp[(l,r)] = max(dp[(l,r)], coins)
            return dp[(l,r)]

        return dfs(1,len(nums)- 2)
```

```python
# Iterative solution
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        # Add 1 at both ends for boundary conditions
        nums = [1] + nums + [1]
        n = len(nums)
        # Create a DP table with (n x n) initialized to 0
        dp = [[0] * n for _ in range(n)]

        # Fill the DP table
        # l is the length of the subarray considered
        for l in range(1, n-1):  # l ranges from 1 to n-2 since nums has been padded with 1's
            for i in range(1, n-l):
                j = i + l - 1
                # Find the best k to split on
                for k in range(i, j+1):
                    # Calculate the max coins by making k the last balloon to burst
                    coins = nums[i-1] * nums[k] * nums[j+1]
                    coins += dp[i][k-1] + dp[k+1][j]
                    dp[i][j] = max(dp[i][j], coins)

        # The result is found in the DP table from 1 to n-2 (1-based index of the original nums)
        return dp[1][n-2]

```

## Thoughts

Hands down one of the hardest problems that I have come across. Needs review

### Time Complexity

O(n^3), where `n` is the number of balloons. This complexity arises from the three nested loops: iterating over all subarrays, iterating over all possible `k` for each subarray, and calculating the maximum coins.

### Space Complexity

O(n^2) for the DP table.
