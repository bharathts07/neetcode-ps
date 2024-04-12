# [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string `s`, return *the longest* *palindromic substring* in `s`.

**Example 1:**

**Input:** s = "babad"
**Output:** "bab"
**Explanation:** "aba" is also a valid answer.

**Example 2:**

**Input:** s = "cbbd"
**Output:** "bb"

## **Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

## Solution

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def expandAroundCenter(left: int, right: int) -> str:
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            # Return the palindrome, not including the last expanded characters that broke the while loop
            return s[left + 1:right]

        longest = ""
        for i in range(len(s)):
            # Odd length palindromes: expand around single character
            odd_pal = expandAroundCenter(i, i)
            if len(odd_pal) > len(longest):
                longest = odd_pal

            # Even length palindromes: expand around pair of characters
            if i + 1 < len(s):
                even_pal = expandAroundCenter(i, i + 1)
                if len(even_pal) > len(longest):
                    longest = even_pal

        return longest

```

## Thoughts

There is a linear but very complex algorithm called manacher algorithm, but it us not usually asked.

### Time Complexity

The time complexity is O(n^2) in the worst case, where n is the length of the string s. This occurs when we need to check each possible center and potentially expand the full length of the string for palindromes.

### Space Complexity

The space complexity is O(1). We only need constant extra space to store the current longest palindrome and indices while expanding around centers. We're not using any additional data structures that scale with the input size.
