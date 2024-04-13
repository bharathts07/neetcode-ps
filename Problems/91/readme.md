# [91. Decode Ways](https://leetcode.com/problems/decode-ways/)

A message containing letters from `A-Z` can be **encoded** into numbers using the following mapping:

'A' -> "1"
'B' -> "2"
...
'Z' -> "26"

To **decode** an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, `"11106"` can be mapped into:

- `"AAJF"` with the grouping `(1 1 10 6)`
- `"KJF"` with the grouping `(11 10 6)`

Note that the grouping `(1 11 06)` is invalid because `"06"` cannot be mapped into `'F'` since `"6"` is different from `"06"`.

Given a string `s` containing only digits, return *the **number** of ways to **decode** it*.

The test cases are generated so that the answer fits in a **32-bit** integer.

**Example 1:**

**Input:** s = "12"
**Output:** 2
**Explanation:** "12" could be decoded as "AB" (1 2) or "L" (12).

**Example 2:**

**Input:** s = "226"
**Output:** 3
**Explanation:** "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).

**Example 3:**

**Input:** s = "06"
**Output:** 0
**Explanation:** "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").

## **Constraints:**

- `1 <= s.length <= 100`
- `s` contains only digits and may contain leading zero(s).

## Solution

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        if not s or s[0] == '0':
            return 0

        # Length of the string
        n = len(s)

        # dp[i] represents the number of ways to decode s[:i]
        dp = [0] * (n + 1)
        dp[0], dp[1] = 1, 1

        for i in range(2, n + 1):
            # Single character decoding (must not be '0')
            if s[i-1] != '0':
                dp[i] += dp[i-1]

            # Double character decoding (must be between 10 to 26)
            two_digit = int(s[i-2:i])  # Convert the two characters to an integer
            if 10 <= two_digit <= 26:
                dp[i] += dp[i-2]

        return dp[n]

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(n), where n is the length of the string s. This is because we traverse the string once and perform constant-time operations for each character.

### Space Complexity

The space complexity is O(n) due to the use of the dp array to store the number of decoding ways for each substring up to i.
