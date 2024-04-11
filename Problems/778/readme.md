# [778. Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/)

You are given an `n x n` integer matrix `grid` where each value `grid[i][j]` represents the elevation at that point `(i, j)`.

The rain starts to fall. At time `t`, the depth of the water everywhere is `t`. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most `t`. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.

Return *the least time until you can reach the bottom right square* `(n - 1, n - 1)` *if you start at the top left square* `(0, 0)`.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/06/29/swim1-grid.jpg)

**Input:** grid = [[0,2],[1,3]]
**Output:** 3
Explanation:
At time 0, you are in grid location (0, 0).
You cannot go anywhere else because 4-directionally adjacent neighbors have a higher elevation than t = 0.
You cannot reach point (1, 1) until time 3.
When the depth of water is 3, we can swim anywhere inside the grid.

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2021/06/29/swim2-grid-1.jpg)

**Input:** grid = [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]
**Output:** 16
**Explanation:** The final route is shown.
We need to wait until time 16 so that (0, 0) and (4, 4) are connected.

## **Constraints:**

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 50`
- `0 <= grid[i][j] < n2`
- Each value `grid[i][j]` is **unique**.

## Solution

### Approach 1 : Using heap

```python
import heapq

class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        n = len(grid)
        visited = [[False] * n for _ in range(n)]
        min_heap = [(grid[0][0], 0, 0)]  # (time, x, y)
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        while min_heap:
            time, x, y = heapq.heappop(min_heap)
            if x == n - 1 and y == n - 1:
                return time
            visited[x][y] = True
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n and not visited[nx][ny]:
                    new_time = max(time, grid[nx][ny])
                    heapq.heappush(min_heap, (new_time, nx, ny))
```

this code makes some optimizations

```python
import heapq

class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        n = len(grid)
        time = [[float('inf')] * n for _ in range(n)]
        time[0][0] = grid[0][0]
        min_heap = [(grid[0][0], 0, 0)]  # (time, x, y)
        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        while min_heap:
            current_time, x, y = heapq.heappop(min_heap)
            if x == n - 1 and y == n - 1:
                return current_time
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    new_time = max(current_time, grid[nx][ny])
                    if new_time < time[nx][ny]:
                        time[nx][ny] = new_time
                        heapq.heappush(min_heap, (new_time, nx, ny))

```

### Approach 2 : Using a binary search + DFS

```python
class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        n = len(grid)

        def can_swim(t):
            visited = [[False] * n for _ in range(n)]
            directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

            def dfs(x, y):
                if x == n - 1 and y == n - 1:
                    return True
                visited[x][y] = True
                for dx, dy in directions:
                    nx, ny = x + dx, y + dy
                    if 0 <= nx < n and 0 <= ny < n and not visited[nx][ny] and grid[nx][ny] <= t:
                        if dfs(nx, ny):
                            return True
                return False

            return dfs(0, 0)

        left, right = grid[0][0], n * n - 1
        while left < right:
            mid = (left + right) // 2
            if can_swim(mid):
                right = mid
            else:
                left = mid + 1

        return left

```

## Thoughts

### 1 approach

Revist this aprroach as I got time limit exceeded with the above code.

#### Time Complexity

The time complexity is O(N^2 log N), where N is the size of the grid. This is because, in the worst case, we need to push and pop each cell in the min-heap, and each heap operation takes O(log N) time.

#### Space Complexity

The space complexity is O(N^2) for the visited matrix and the min-heap.

### 2 approach

#### Time Complexity for 2

The time complexity is O(N^2 log N), where N is the size of the grid. The binary search takes O(log N) iterations, and each DFS/BFS check takes O(N^2) time.

### Space Complexity for 2

The space complexity is O(N^2) for the visited matrix used in the DFS/BFS function.
