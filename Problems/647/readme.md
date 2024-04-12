# [647. Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)

Given a string `s`, return *the number of **palindromic substrings** in it*.

A string is a **palindrome** when it reads the same backward as forward.

A **substring** is a contiguous sequence of characters within the string.

**Example 1:**

**Input:** s = "abc"
**Output:** 3
**Explanation:** Three palindromic strings: "a", "b", "c".

**Example 2:**

**Input:** s = "aaa"
**Output:** 6
**Explanation:** Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

## **Constraints:**

- `1 <= s.length <= 1000`
- `s` consists of lowercase English letters.

## Solution

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        def countPalindromesAroundCenter(left: int, right: int) -> int:
            count = 0
            while left >= 0 and right < len(s) and s[left] == s[right]:
                count += 1
                left -= 1
                right += 1
            return count

        total_count = 0
        for i in range(len(s)):
            # Count odd length palindromes centered at s[i]
            total_count += countPalindromesAroundCenter(i, i)

            # Count even length palindromes centered between s[i] and s[i + 1]
            total_count += countPalindromesAroundCenter(i, i + 1)

        return total_count

```

## Thoughts

### Time Complexity

The time complexity is O(n^2) in the worst case, where n is the length of the string s. This occurs when we need to check each possible center and potentially expand the full length of the string for palindromes.

### Space Complexity

The space complexity is O(1).
