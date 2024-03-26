# 1. Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]

## Constraints

2 <= nums.length <= 10^4
-10^9 <= nums[i] <= 10^9
-10^9 <= target <= 10^9
Only one valid answer exists.

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

## Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(0,len(nums),1):
            for j in range(len(nums)-1,-1,-1): 
                if i!=j and nums[i]+nums[j] == target:
                    return [i,j]
```

This is O(n^2) time complexity solution and O(1) space

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Create an empty dictionary to store the index of each element.
        # The key will be the element value, and the value will be the index.
        indices = {}

        # Iterate through the list of numbers.
        for i, num in enumerate(nums):
            # Calculate the complement of the current number.
            # This is the value that, when added to the current number, equals the target.
            complement = target - num

            # Check if the complement is already in the dictionary.
            if complement in indices:
                # If it is, we have found the two numbers that add up to the target.
                # Return the indices of these two numbers.
                return [indices[complement], i]

            # If the complement is not in the dictionary, add the current number and its index to the dictionary.
            indices[num] = i

        # If no solution is found (which should not happen in this problem), return an empty list.
        return []

```

## Thoughts

IT seemed like a much more complicated problem that it actaully was. Using brute force approach gives an O(n^2) time complexity with contant space.

For a slightly better solution you can use a map to store the element and its index. You can then search if the remaining element to add up to the target exists in the dictionary. This newer solutions will have O(n) Time complexity with O(n) Space complexity for the map.
