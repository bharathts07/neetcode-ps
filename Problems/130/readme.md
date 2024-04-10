# [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

Given an `m x n` matrix `board` containing `'X'` and `'O'`, *capture all regions that are 4-directionally surrounded by* `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

**Input:** board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
**Output:** [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
**Explanation:** Notice that an 'O' should not be flipped if:

- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
  The bottom 'O' is on the border, so it is not flipped.
  The other three 'O' form a surrounded region, so they are flipped.

**Example 2:**

**Input:** board = [["X"]]
**Output:** [["X"]]

## **Constraints:**

- `m == board.length`
- `n == board[i].length`
- `1 <= m, n <= 200`
- `board[i][j]` is `'X'` or `'O'`.

## Solution

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        if not board:
            return

        def dfs(row, col):
            if 0 <= row < len(board) and 0 <= col < len(board[0]) and board[row][col] == 'O':
                board[row][col] = 'T'  # Mark as temporarily safe
                for dr, dc in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                    dfs(row + dr, col + dc)

        # Mark border-connected 'O's
        for i in range(len(board)):
            dfs(i, 0)
            dfs(i, len(board[0]) - 1)
        for j in range(len(board[0])):
            dfs(0, j)
            dfs(len(board) - 1, j)

        # Capture surrounded regions
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == 'O':
                    board[i][j] = 'X'

        # Restore border-connected 'O's
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == 'T':
                    board[i][j] = 'O'

```

## Thoughts

### Time Complexity

The time complexity is O(M \* N), where M is the number of rows and N is the number of columns in the board. This is because, in the worst case, we might need to visit every cell in the board once.

### Space Complexity

The space complexity is O(M \* N) in the worst case for the recursion stack, in case the board is filled with 'O's. However, this can be considered O(1) if we assume the recursion stack size is limited by the system.
