# [329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

Given an `m x n` integers `matrix`, return *the length of the longest increasing path in* `matrix`.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/01/05/grid1.jpg)

**Input:** matrix = [[9,9,4],[6,6,8],[2,1,1]]
**Output:** 4
**Explanation:** The longest increasing path is `[1, 2, 6, 9]`.

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2021/01/27/tmp-grid.jpg)

**Input:** matrix = [[3,4,5],[3,2,6],[2,2,1]]
**Output:** 4
**Explanation:** The longest increasing path is `[3, 4, 5, 6]`. Moving diagonally is not allowed.

**Example 3:**

**Input:** matrix = [[1]]
**Output:** 1

## **Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- `0 <= matrix[i][j] <= 231 - 1`

## Solution

```python
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        if not matrix or not matrix[0]:
            return 0

        m, n = len(matrix), len(matrix[0])
        memo = [[0] * n for _ in range(m)]

        def dfs(i, j):
            # If already computed, return the stored value
            if memo[i][j] != 0:
                return memo[i][j]

            # Possible moves: right, left, down, up
            directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
            max_length = 1
            for di, dj in directions:
                ni, nj = i + di, j + dj
                if 0 <= ni < m and 0 <= nj < n and matrix[ni][nj] > matrix[i][j]:
                    max_length = max(max_length, 1 + dfs(ni, nj))

            memo[i][j] = max_length
            return max_length

        longest_path = 0
        for i in range(m):
            for j in range(n):
                if memo[i][j] == 0:
                    longest_path = max(longest_path, dfs(i, j))

        return longest_path

```

## Thoughts

### Time Complexity

O(m×n). In the worst case, the DFS for each cell is only computed once thanks to memoization. Each cell effectively participates in DFS exactly once.

### Space Complexity

O(m×n) due to the space used by the recursion stack (in the worst case, the path could be as long as m×n cells) and the memoization table.
