# [78. Subsets](https://leetcode.com/problems/subsets/)

Given an integer array `nums` of **unique** elements, return *all possible* *subsets* _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

**Example 2:**

**Input:** nums = [0]
**Output:** [[],[0]]

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

## Solution

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        def backtrack(start, path):
            # Add the current subset to the result
            result.append(path.copy())
            # Explore further subsets
            for i in range(start, len(nums)):
                path.append(nums[i])
                backtrack(i + 1, path)
                path.pop()

        result = []
        backtrack(0, [])
        return result


```

## Thoughts

Explanation in neetcode is way better and more intuitive, refer that.

### Time Complexity

The time complexity of this solution is O(2^N), where N is the number of elements in the input list. This is because, for each element, we have two choices (include or exclude), leading to 2^N possible subsets.

### Space Complexity

The space complexity is also O(2^N), considering the space required to store all the subsets. Additionally, the recursion stack will use O(N) space in the worst case.
