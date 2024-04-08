# [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

**Input:** candidates = [10,1,2,7,6,1,5], target = 8
**Output:**
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

**Example 2:**

**Input:** candidates = [2,5,2,1,2], target = 5
**Output:**
[
[1,2,2],
[5]
]

## **Constraints:**

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

## Solution

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        def backtrack(start, path, remaining):
            if remaining == 0:
                result.append(path.copy())
                return
            for i in range(start, len(candidates)):
                # Skip duplicates
                if i > start and candidates[i] == candidates[i - 1]:
                    continue
                # Skip if the remaining target would be negative
                if candidates[i] > remaining:
                    break
                path.append(candidates[i])
                backtrack(i + 1, path, remaining - candidates[i])
                path.pop()

        candidates.sort()  # Sort the array to handle duplicates
        result = []
        backtrack(0, [], target)
        return result

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(2^N) in the worst case, where N is the number of elements in the input array. This is because, in the worst case, we might need to explore all possible combinations.

### Space Complexity

The space complexity is O(N) for the recursion stack. Additionally, the space required to store the result is not counted towards the space complexity of the algorithm.
