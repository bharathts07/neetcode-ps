# [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

Given two strings s and t, return *the number of distinct* **_subsequences_** *of* s *which equals* t.

The test cases are generated so that the answer fits on a 32-bit signed integer.

**Example 1:**

**Input:** s = "rabbbit", t = "rabbit"
**Output:** 3
**Explanation:**
As shown below, there are 3 ways you can generate "rabbit" from s.
`**rabb**b**it**`
`**ra**b**bbit**`
`**rab**b**bit**`

**Example 2:**

**Input:** s = "babgbag", t = "bag"
**Output:** 5
**Explanation:**
As shown below, there are 5 ways you can generate "bag" from s.
`**ba**b**g**bag`
`**ba**bgba**g**`
`**b**abgb**ag**`
`ba**b**gb**ag**`
`babg**bag**`

## **Constraints:**

- `1 <= s.length, t.length <= 1000`
- `s` and `t` consist of English letters.

## Solution

```python
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        m, n = len(s), len(t)
        dp = [[0] * (n + 1) for _ in range(m + 1)]

        # Initializing the base case
        for i in range(m + 1):
            dp[i][0] = 1  # An empty t can be formed by deleting all characters from any prefix of s

        # Fill dp table
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                # If characters match, consider both including and excluding s[i-1]
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j]

        return dp[m][n]

```

## Thoughts

Kinda difficult, need to review again

- If the characters match, it opens up two possibilities:
  - **Include `s[i-1]` in the subsequence**: If you decide to use the `i-th` character of `s` to match the `j-th` character of `t`, then you effectively reduce the problem to finding the number of ways to match the first `j-1` characters of `t` with the first `i-1` characters of `s`. Hence, you add `dp[i-1][j-1]` to your current count.
  - **Exclude `s[i-1]` from the subsequence**: Even though `s[i-1]` matches `t[j-1]`, you might choose not to use this character. In this case, the problem reduces to matching the first `j` characters of `t` with the first `i-1` characters of `s`. Therefore, you also add `dp[i-1][j]` to your current count.
- If the characters do not match, you cannot use `s[i-1]` to match `t[j-1]`.
  - The only choice is to exclude `s[i-1]`.
  - The problem then reduces to finding the number of ways to match the first `j` characters of `t` with the first `i-1` characters of `s`.

### Time Complexity

O(m×n), where `m` is the length of `s` and `n` is the length of `t`. This complexity arises from the nested loops required to fill the `dp` table.

### Space Complexity

O(m×n) for the `dp` table. This can be optimized to O(n) by noting that `dp[i][j]` only depends on the previous row `dp[i-1][..]`
