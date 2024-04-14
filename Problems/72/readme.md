# [72. Edit Distance](https://leetcode.com/problems/edit-distance/)

Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"
**Output:** 3
**Explanation:**
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"
**Output:** 5
**Explanation:**
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')

## **Constraints:**

- `0 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of lowercase English letters.

## Solution

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = [[0] * (n + 1) for _ in range(m + 1)]

        # Base cases initialization
        for i in range(1, m + 1):
            dp[i][0] = i  # Cost of deleting all characters from word1[0:i]
        for j in range(1, n + 1):
            dp[0][j] = j  # Cost of inserting all characters to form word2[0:j]

        # Fill the dp table
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]  # No operation needed
                else:
                    dp[i][j] = min(dp[i - 1][j] + 1,    # Delete
                                   dp[i][j - 1] + 1,    # Insert
                                   dp[i - 1][j - 1] + 1)  # Replace

        return dp[m][n]

```

## Thoughts

### Time Complexity

O(m×n), where `m` is the length of `word1` and `n` is the length of `word2`. This complexity arises from the nested loops required to fill the DP table.

### Space Complexity

O(m×n) for the DP table. This can be optimized to O(n) using a rolling array technique if minimizing space is critical, by maintaining only the current and the previous row of the DP table.
