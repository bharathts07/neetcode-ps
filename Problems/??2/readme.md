# [Islands and Treasure](https://neetcode.io/problems/islands-and-treasure)

You are given a m×n 2D `grid` initialized with these three possible values:

1. `-1` - A water cell that *can not* be traversed.
2. `0` - A treasure chest.
3. `INF` - A land cell that *can* be traversed. We use the integer `2^31 - 1 = 2147483647` to represent `INF`.

Fill each land cell with the distance to its nearest treasure chest. If a land cell cannot reach a treasure chest than the value should remain `INF`.

Assume the grid can only be traversed up, down, left, or right.

**Example 1:**

```java
Input: [
  [2147483647,-1,0,2147483647],
  [2147483647,2147483647,2147483647,-1],
  [2147483647,-1,2147483647,-1],
  [0,-1,2147483647,2147483647]
]

Output: [
  [3,-1,0,1],
  [2,2,1,-1],
  [1,-1,2,-1],
  [0,-1,3,4]
]
```

**Example 2:**

```java
Input: [
  [0,-1],
  [2147483647,2147483647]
]

Output: [
  [0,-1],
  [1,2]
]
```

## **Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 100`
- `grid[i][j]` is one of `{-1, 0, 2147483647}`

## Solution

```python
from collections import deque

class Solution:
    def islandsAndTreasure(self, grid: List[List[int]]) -> None:
        rows, cols = len(grid), len(grid[0])
        queue = deque()

        # Initialize queue with treasure chests
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 0:
                    queue.append((r, c, 0))  # (row, col, distance)

        # BFS
        directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
        while queue:
            r, c, distance = queue.popleft()
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 2147483647:
                    grid[nr][nc] = distance + 1
                    queue.append((nr, nc, distance + 1))

        # No need to return the grid as it is modified in-place
```

## Thoughts

### Time Complexity

The time complexity is O(M \* N), where M is the number of rows and N is the number of columns in the grid. This is because, in the worst case, we might need to visit every cell in the grid once.

### Space Complexity

The space complexity is O(M \* N) for the queue used in the BFS. In the worst case, the queue might contain all the cells in the grid.
