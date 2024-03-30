# [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.

**Example 2:**

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

## **Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`

## Solution

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        # Initialize variables
        char_count = {}  # Dictionary to store the count of each character in the current window
        max_length = 0   # Length of the longest valid substring found so far
        max_freq = 0     # Count of the most frequent character in the current window
        left = 0         # Left pointer of the window

        # Iterate through the string with the right pointer
        for right in range(len(s)):
            # Update the count of the current character
            current_char = s[right]
            if current_char in char_count:
                char_count[current_char] += 1
            else:
                char_count[current_char] = 1
            
            # Update the count of the most frequent character in the window
            max_freq = max(max_freq, char_count[current_char])

            # Check if the current window is valid (number of replacements <= k)
            while (right - left + 1) - max_freq > k:
                # If not valid, shrink the window from the left
                char_to_remove = s[left]
                char_count[char_to_remove] -= 1
                left += 1

            # Update the length of the longest valid substring
            window_size = right - left + 1
            max_length = max(max_length, window_size)

        return max_length

```

## Thoughts

I'm stumped. Had to look at the solution. The inner while loop to move the left pointer is still pretty confusing. Need to revist after finishing all other problems.

Time Complexity = O(n)
Space complexity = O(26) Capital letters in english.
