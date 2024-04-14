# [55. Jump Game](https://leetcode.com/problems/jump-game/)

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` *if you can reach the last index, or* `false` *otherwise*.

**Example 1:**

**Input:** nums = [2,3,1,1,4]
**Output:** true
**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [3,2,1,0,4]
**Output:** false
**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

## **Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`

## Solution

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        maxReach = 0  # Initially, the furthest we can reach is the start index

        for i in range(len(nums)):
            if i > maxReach:
                # If the current index is beyond the maximum reach, it's not possible to proceed
                return False
            # Update the maximum reach
            maxReach = max(maxReach, i + nums[i])
            if maxReach >= len(nums) - 1:
                # If at any point the maximum reach surpasses or reaches the last index, we can succeed
                return True

        # After the loop, check if we've reached the last index
        return maxReach >= len(nums) - 1

```

## Thoughts

### Time Complexity

O(n) - We only traverse the array once, making this solution linear in terms of the number of elements in the array.

### Space Complexity

O(1) - We use a constant amount of extra space, as only a few variables are required regardless of input size.
