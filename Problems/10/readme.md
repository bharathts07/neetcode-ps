# [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

- `'.'` Matches any single character.​​​​
- `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"
**Output:** false
**Explanation:** "a" does not match the entire string "aa".

**Example 2:**

**Input:** s = "aa", p = "a*"
**Output:** true
**Explanation:** '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".

**Example 3:**

**Input:** s = "ab", p = "._"
**Output:** true
**Explanation:** "._" means "zero or more (\*) of any character (.)".

## **Constraints:**

- `1 <= s.length <= 20`
- `1 <= p.length <= 20`
- `s` contains only lowercase English letters.
- `p` contains only lowercase English letters, `'.'`, and `'*'`.
- It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        m, n = len(s), len(p)
        # Create a dp table with dimensions (m+1)x(n+1) for 1-based indexing
        dp = [[False] * (n + 1) for _ in range(m + 1)]

        # Base case: empty string and empty pattern are a match
        dp[0][0] = True

        # Initialize dp for patterns that can match an empty string (like a*, a*b*, etc.)
        for j in range(2, n + 1):
            if p[j - 1] == '*':
                # A '*' can nullify the character before it, hence check two positions back
                dp[0][j] = dp[0][j - 2]

        # Fill the dp table
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                # If the current characters match or if there's a '.', check the diagonally previous value
                if p[j - 1] == s[i - 1] or p[j - 1] == '.':
                    dp[i][j] = dp[i - 1][j - 1]
                # If there's a '*', there are two cases to consider
                elif p[j - 1] == '*':
                    # Case 1: Treat '*' and its preceding character as empty (remove both)
                    dp[i][j] = dp[i][j - 2]
                    # Case 2: If the character before '*' can match s[i-1], propagate the value from the previous row
                    if p[j - 2] == s[i - 1] or p[j - 2] == '.':
                        dp[i][j] = dp[i][j] or dp[i - 1][j]

        # The bottom-right cell contains the answer for the full strings
        return dp[m][n]

```

## Thoughts

Really hard problem again. Needs review with edge cases.

### Time Complexity

O(m×n), where `m` is the length of the string `s` and `n` is the length of the pattern `p`. This time complexity arises because each cell in the `dp` table needs to be filled exactly once.

### Space Complexity

O(m×n) due to the space used by the `dp` table. This could potentially be reduced to O(n) by only keeping the last row of the `dp` table if space optimization is required.
