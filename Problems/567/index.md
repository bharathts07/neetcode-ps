# [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

Given two strings `s1` and `s2`, return `true` _if_ `s2` _contains a permutation of_ `s1`_, or_ `false` _otherwise_.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**

**Input:** s1 = "ab", s2 = "eidbaooo"
**Output:** true
**Explanation:** s2 contains one permutation of s1 ("ba").

**Example 2:**

**Input:** s1 = "ab", s2 = "eidboaoo"
**Output:** false

## **Constraints:**

- `1 <= s1.length, s2.length <= 104`
- `s1` and `s2` consist of lowercase English letters.

## Solution

```python
class Solution:
    def get_char_index(self, char: str) -> int:
        # Convert a character to its corresponding index (0-25 for 'a'-'z')
        return ord(char) - ord('a')

    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2):
            return False

        # Initialize the character count for s1 and the current window in s2
        s1_count = [0] * 26
        window_count = [0] * 26

        # Update the character count for s1
        for char in s1:
            s1_count[self.get_char_index(char)] += 1

        # Initialize the first window in s2
        for i in range(len(s1)):
            window_count[self.get_char_index(s2[i])] += 1

        # Slide the window over s2 and check for matches with s1's character count
        for i in range(len(s1), len(s2)):
            if s1_count == window_count:
                return True
            # Remove the character going out of the window
            char_to_remove = s2[i - len(s1)]
            window_count[self.get_char_index(char_to_remove)] -= 1
            # Add the new character coming into the window
            char_to_add = s2[i]
            window_count[self.get_char_index(char_to_add)] += 1

        # Check the last window
        return s1_count == window_count

```

## Thoughts

Learnt a new syntax in python about initializing a list of repeated elements and about range functions involving start and stop values. Kind of straightforward question.

Time complexity = O(m) , length of s2 string in which you try to find the permuted substring.
Space complexity = O(1) , constant as we use 2 data structure for count list of characters.
