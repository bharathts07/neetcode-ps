# [46. Permutations](https://leetcode.com/problems/permutations/)

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]
**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]
**Output:** [[1]]

## **Constraints:**

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

## Solution

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        def backtrack(start):
            # Base case: if the permutation is complete, add it to the result
            if start == len(nums):
                result.append(nums.copy())
                return
            # Recursive case: generate permutations by swapping elements
            for i in range(start, len(nums)):
                nums[start], nums[i] = nums[i], nums[start]
                backtrack(start + 1)
                nums[start], nums[i] = nums[i], nums[start]

        result = []
        backtrack(0)
        return result

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(N!), where N is the number of elements in the input array. This is because there are N! possible permutations.

### Space Complexity

The space complexity is O(N) for the recursion stack. In addition, the space required to store the result is not counted towards the space complexity of the algorithm.
