# [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the

frequency

of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7
**Output:** [[2,2,3],[7]]
**Explanation:**
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8
**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1
**Output:** []

## **Constraints:**

- `1 <= candidates.length <= 30`
- `2 <= candidates[i] <= 40`
- All elements of `candidates` are **distinct**.
- `1 <= target <= 40`

## Solution

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        def backtrack(start, path, remaining):
            # Base case: if the remaining target is 0, add the path to the result
            if remaining == 0:
                result.append(path.copy())
                return
            # Recursive case: try adding each candidate to the path
            for i in range(start, len(candidates)):
                if candidates[i] <= remaining:
                    path.append(candidates[i])
                    backtrack(i, path, remaining - candidates[i])
                    path.pop()

        result = []
        backtrack(0, [], target)
        return result

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(N^(T/M + 1)), where N is the number of candidates, T is the target value, and M is the minimal value among the candidates. This is because, in the worst case, we might need to explore each candidate up to T/M times.

### Space Complexity

The space complexity is O(T/M) for the recursion stack, as in the worst case, we might have a combination where we use the smallest candidate T/M times.
