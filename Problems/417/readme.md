# [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

There is an `m x n` rectangular island that borders both the **Pacific Ocean** and **Atlantic Ocean**. The **Pacific Ocean** touches the island's left and top edges, and the **Atlantic Ocean** touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an `m x n` integer matrix `heights` where `heights[r][c]` represents the **height above sea level** of the cell at coordinate `(r, c)`.

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is **less than or equal to** the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return *a **2D list** of grid coordinates* `result` *where* `result[i] = [ri, ci]` *denotes that rain water can flow from cell* `(ri, ci)` *to **both** the Pacific and Atlantic oceans*.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/06/08/waterflow-grid.jpg)

**Input:**

```python
heights = [
    [1,2,2,3,5],
    [3,2,3,4,4],
    [2,4,5,3,1],
    [6,7,1,4,5],
    [5,1,1,2,4]
    ]
```

**Output:** [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
**Explanation:** The following cells can flow to the Pacific and Atlantic oceans, as shown below:
[0,4]: [0,4] -> Pacific Ocean
  [0,4] -> Atlantic Ocean
[1,3]: [1,3] -> [0,3] -> Pacific Ocean
  [1,3] -> [1,4] -> Atlantic Ocean
[1,4]: [1,4] -> [1,3] -> [0,3] -> Pacific Ocean
  [1,4] -> Atlantic Ocean
[2,2]: [2,2] -> [1,2] -> [0,2] -> Pacific Ocean
  [2,2] -> [2,3] -> [2,4] -> Atlantic Ocean
[3,0]: [3,0] -> Pacific Ocean
  [3,0] -> [4,0] -> Atlantic Ocean
[3,1]: [3,1] -> [3,0] -> Pacific Ocean
  [3,1] -> [4,1] -> Atlantic Ocean
[4,0]: [4,0] -> Pacific Ocean
[4,0] -> Atlantic Ocean
Note that there are other possible paths for these cells to flow to the Pacific and Atlantic oceans.

**Example 2:**

**Input:** heights = [[1]]
**Output:** [[0,0]]
**Explanation:** The water can flow from the only cell to the Pacific and Atlantic oceans.

## **Constraints:**

- `m == heights.length`
- `n == heights[r].length`
- `1 <= m, n <= 200`
- `0 <= heights[r][c] <= 105`

## Solution

```python
class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        if not heights or not heights[0]:
            return []

        def dfs(row, col, visited, prevHeight):
            if (row, col) in visited or row < 0 or col < 0 or row >= len(heights) or col >= len(heights[0]) or heights[row][col] < prevHeight:
                return
            visited.add((row, col))
            for dr, dc in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                dfs(row + dr, col + dc, visited, heights[row][col])

        pacific = set()
        atlantic = set()
        for i in range(len(heights)):
            dfs(i, 0, pacific, float('-inf'))
            dfs(i, len(heights[0]) - 1, atlantic, float('-inf'))
        for j in range(len(heights[0])):
            dfs(0, j, pacific, float('-inf'))
            dfs(len(heights) - 1, j, atlantic, float('-inf'))

        return list(pacific & atlantic)
```

## Thoughts

### Time Complexity

The time complexity is O(M \* N), where M is the number of rows and N is the number of columns in the grid. This is because, in the worst case, we might need to visit every cell in the grid once for each ocean.

### Space Complexity

The space complexity is O(M \* N) for the visited sets and the recursion stack. In the worst case, all cells might be added to the sets and the recursion stack.
