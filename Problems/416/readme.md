# [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

Given an integer array `nums`, return `true` *if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or* `false` *otherwise*.

**Example 1:**

**Input:** nums = [1,5,11,5]
**Output:** true
**Explanation:** The array can be partitioned as [1, 5, 5] and [11].

**Example 2:**

**Input:** nums = [1,2,3,5]
**Output:** false
**Explanation:** The array cannot be partitioned into equal sum subsets.

## **Constraints:**

- `1 <= nums.length <= 200`
- `1 <= nums[i] <= 100`

## Solution

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        total_sum = sum(nums)

        # If total sum is odd, it's not possible to partition it into two equal sum subsets
        if total_sum % 2 != 0:
            return False

        target = total_sum // 2
        dp = [False] * (target + 1)
        dp[0] = True  # Base case: zero sum is always possible

        for num in nums:
            for j in range(target, num - 1, -1):
                if dp[j - num]:
                    dp[j] = True

        return dp[target]


```

## Thoughts

Problem is made much easier becasue of the contraint that numbers are less than 100 and that the list if numbers is less than 100.

### Time Complexity

O(n \* target) where n is the number of elements in nums and target is total_sum / 2. This is because we potentially iterate through the DP array target + 1 times for each number in nums.

### Space Complexity

O(target), where target is total_sum / 2. The space is used by the dp array that keeps track of possible sums up to target.

## Approach 2 using set

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        total_sum = sum(nums)

        # Early exit if the total sum is odd
        if total_sum % 2 != 0:
            return False

        target = total_sum // 2
        possible_sums = {0}

        for num in nums:
            new_sums = set()
            for s in possible_sums:
                new_sum = s + num
                if new_sum == target:
                    return True
                new_sums.add(new_sum)
            possible_sums.update(new_sums)

        return target in possible_sums

```

### Time Complexity-2

O(n \* m), where n is the number of elements in nums and m is the number of unique sums that can be generated. In the worst case, this could be as many as the sum of combinations of elements, which would be substantial but typically much less than the maximum potential sums (which would be the product of element count and maximum element value).

### Space Complexity-2

O(m), where m is the number of unique sums. This approach can be more space-efficient compared to the DP array when the number of unique possible sums is less than the target sum, particularly when the elements have a large range or the target sum is very large.
