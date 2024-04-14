# [494. Target Sum](https://leetcode.com/problems/target-sum/)

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3
**Output:** 5
**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3.

```python
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**Example 2:**

**Input:** nums = [1], target = 1
**Output:** 1

## **Constraints:**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

## Solution

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        memo = {}

        def dp(index, current_sum):
            if index == len(nums):
                return 1 if current_sum == target else 0

            # Use memoization to avoid recomputation
            if (index, current_sum) in memo:
                return memo[(index, current_sum)]

            # Calculate the number of ways by considering both adding and subtracting the current number
            add = dp(index + 1, current_sum + nums[index])
            subtract = dp(index + 1, current_sum - nums[index])

            memo[(index, current_sum)] = add + subtract
            return memo[(index, current_sum)]

        return dp(0, 0)

```

## Thoughts

### Time Complexity

O(n×S), where n is the number of elements in nums and S is the range of possible sums (which can be large, depending on the inputs). Memoization helps ensure that each state is computed at most once.

### Space Complexity

O(n×S) for the memoization table, which might store a state for each combination of index and possible sum.

## A more efficient un-intuitive solutions

Transform the problem to subset sum problem and account for edge cases.

The problem of finding the number of ways to assign `+` and `-` symbols to generate a target sum from a list of numbers can be approached as a variant of the subset sum problem, specifically as a "count of subset sums" with a twist involving both positive and negative sums.

The sum of all elements with `+` and `-` can be viewed in terms of two subsets, `S1` and `S2`, where:

- `S1` includes elements assigned with `+`.
- `S2` includes elements assigned with `-`.

Given this, the expression formed as `S1 - S2 = target` can be rearranged.

`S1 = (sum(nums) + target ) / 2`

This reveals that the task is equivalent to finding the number of ways to select a subset of `nums` that sums to `(sum(nums) + target) / 2`.

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        total_sum = sum(nums)
        if (total_sum + target) % 2 != 0 or total_sum < target or (total_sum + target) < 0:
            return 0

        sum_p = (total_sum + target) // 2
        dp = [0] * (sum_p + 1)
        dp[0] = 1  # One way to make sum 0, use no elements

        for num in nums:
            for j in range(sum_p, num - 1, -1):
                dp[j] += dp[j - num]

        return dp[sum_p]

```

### Time Complexity2

- **O(n \times m)**, where `n` is the number of elements in `nums` and `m` is `(sum(nums) + target) / 2`.
  - This complexity arises because we potentially iterate through the `dp` array (whose size is determined by `m`) for each number in `nums`.

### Space Complexity2

- **O(m)**, where `m` is `(sum(nums) + target) / 2`.
  - We use a 1D array `dp` of size `m + 1` to store the count of ways to achieve each sum from `0` to `m`.
