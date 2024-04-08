# [51. N-Queens](https://leetcode.com/problems/n-queens/)

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return \*all distinct solutions to the **n-queens puzzle\***. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4
**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1
**Output:** [["Q"]]

**Constraints:**

- `1 <= n <= 9`

## Solution

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
```

## Thoughts

### Time Complexity

The time complexity remains O(N!) since the main factor is the number of ways to place the queens. However, the constant factor is reduced because the isSafe check is O(1).

### Space Complexity

The space complexity is still O(N^2) for the board, plus O(N) for the recursion stack and the sets. The total space complexity is therefore O(N^2 + 3N) = O(N^2).
