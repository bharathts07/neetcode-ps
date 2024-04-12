# [198. House Robber](https://leetcode.com/problems/house-robber/)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return \*the maximum amount of money you can rob tonight **without alerting the police\***.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** 4
**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

**Example 2:**

**Input:** nums = [2,7,9,3,1]
**Output:** 12
**Explanation:** Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

## Solution

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return nums[0]

        dp = [0] * n
        dp[0], dp[1] = nums[0], max(nums[0], nums[1])

        for i in range(2, n):
            dp[i] = max(dp[i - 1], nums[i] + dp[i - 2])

        return dp[-1]

```

### Optimized Space Complexity

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n == 1:
            return nums[0]

        prev, curr = nums[0], max(nums[0], nums[1])

        for i in range(2, n):
            prev, curr = curr, max(curr, nums[i] + prev)

        return curr

```

In this optimized version, we use two variables prev and curr to keep track of the maximum amounts robbed from the last two houses, eliminating the need for a separate dp array.

## Thoughts

### Time Complexity

The time complexity is O(n), where n is the length of the nums array, as we need to iterate through the array once to fill the dp array.

### Space Complexity

The space complexity is O(n) for the dp array. This can be reduced to O(1) by using two variables to store the maximum amounts robbed from the last two houses instead of using an array.
