# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:**

```python
 grid = [
["1","1","1","1","0"],
["1","1","0","1","0"],
["1","1","0","0","0"],
["0","0","0","0","0"]
]

```

**Output:** 1

**Example 2:**

**Input:**

```python
 grid = [
["1","1","0","0","0"],
["1","1","0","0","0"],
["0","0","1","0","0"],
["0","0","0","1","1"]
]
```

**Output:** 3

## **Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` is `'0'` or `'1'`.

## Solution

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        def dfs(row, col):
            if 0 <= row < len(grid) and 0 <= col < len(grid[0]) and grid[row][col] == '1':
                grid[row][col] = '0'  # Mark as visited
                dfs(row + 1, col)  # Down
                dfs(row - 1, col)  # Up
                dfs(row, col + 1)  # Right
                dfs(row, col - 1)  # Left

        island_count = 0
        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == '1':
                    island_count += 1
                    dfs(row, col)
        return island_count

```

## Thoughts

### Time Complexity

The time complexity is O(M \* N), where M is the number of rows and N is the number of columns in the grid. This is because, in the worst case, we might need to visit every cell in the grid once.

### Space Complexity

The space complexity is O(M \* N) in the worst case for the recursion stack, in case the grid is filled with land cells. However, this can be considered O(1) if we assume the recursion stack size is limited by the system.
