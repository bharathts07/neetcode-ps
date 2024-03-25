# 217. Contains Duplicate

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Example 1:

Input: nums = [1,2,3,1]
Output: true

Example 2:

Input: nums = [1,2,3,4]
Output: false

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true

## Constraints

1 <= nums.length <= 10^5
-10^9 <= nums[i] <= 10^9

## Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        unique_nums = set()
        for num in nums:
            if num in unique_nums:
                return True
            unique_nums.add(num)
        return False
```

## Thoughts

Initially thought had to do some XOR bit magic to save space. Seems that a straightforward solution got accepted.
Time complexity : O(n)
Space Complexity : O(n)
