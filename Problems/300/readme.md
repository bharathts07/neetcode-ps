# [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

Given an integer array `nums`, return *the length of the longest **strictly increasing*** ***subsequence***.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]
**Output:** 4
**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]
**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]
**Output:** 1

**Constraints:**

- `1 <= nums.length <= 2500`
- `-104 <= nums[i] <= 104`

**Follow up:** Can you come up with an algorithm that runs in `O(n log(n))` time complexity?

## Solution

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0

        n = len(nums)
        dp = [1] * n

        for i in range(1, n):
            for j in range(i):
                if nums[j] < nums[i]:
                    dp[i] = max(dp[i], dp[j] + 1)

        return max(dp)

```

## Thoughts

### Time Complexity

O(n^2): The time complexity is quadratic because, for each element nums[i], we potentially compare it with all previous elements nums[j] where j < i. This results in roughly `1/2 * n * (n-1)` comparisons in the worst case.

### Space Complexity

O(n): We need a dp array of size n to store the length of the LIS ending at each index.
