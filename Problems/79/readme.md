# [79. Word Search](https://leetcode.com/problems/word-search/)

Given an `m x n` grid of characters `board` and a string `word`, return `true` *if* `word` *exists in the grid*.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
**Output:** true

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
**Output:** true

**Example 3:**

![e3](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
**Output:** false

## **Constraints:**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` and `word` consists of only lowercase and uppercase English letters.

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

## Solution

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def dfs(row, col, index):
            if index == len(word):
                return True
            if row < 0 or col < 0 or row >= len(board) or col >= len(board[0]) or board[row][col] != word[index]:
                return False
            temp = board[row][col]
            board[row][col] = '#'  # Mark as visited
            found = (dfs(row + 1, col, index + 1) or dfs(row - 1, col, index + 1) or
                     dfs(row, col + 1, index + 1) or dfs(row, col - 1, index + 1))
            board[row][col] = temp  # Backtrack
            return found

        for row in range(len(board)):
            for col in range(len(board[0])):
                if dfs(row, col, 0):
                    return True
        return False

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(M X N X 4^L), where M and N are the dimensions of the board, and L is the length of the word. This is because, in the worst case, we might need to explore all 4 directions for each character in the word.

### Space Complexity

The space complexity is O(L) for the recursion stack, where L is the length of the word. In the worst case, the word could be as long as the number of cells in the board.
