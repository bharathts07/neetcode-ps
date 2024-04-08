# [90. Subsets II](https://leetcode.com/problems/subsets-ii/)

Given an integer array `nums` that may contain duplicates, return *all possible* _subsets_ _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,2]
**Output:** [[],[1],[1,2],[1,2,2],[2],[2,2]]

**Example 2:**

**Input:** nums = [0]
**Output:** [[],[0]]

## **Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`

## Solution

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        def backtrack(start, path):
            result.append(path.copy())
            for i in range(start, len(nums)):
                # Skip duplicates
                if i > start and nums[i] == nums[i - 1]:
                    continue
                path.append(nums[i])
                backtrack(i + 1, path)
                path.pop()

        nums.sort()  # Sort the array to handle duplicates
        result = []
        backtrack(0, [])
        return result

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(2^N), where N is the number of elements in the input array. In the worst case, each element is unique, leading to 2^N possible subsets.

### Space Complexity

The space complexity is O(2^N) for storing the result. The recursion stack will use O(N) space in the worst case.
