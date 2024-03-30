# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window**_

**_substring_**

 _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"
**Output:** "BANC"
**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"
**Output:** "a"
**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"
**Output:** ""
**Explanation:** Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

## **Constraints:**

- `m == s.length`
- `n == t.length`
- `1 <= m, n <= 105`
- `s` and `t` consist of uppercase and lowercase English letters.

**Follow up:** Could you find an algorithm that runs in `O(m + n)` time?

## Solution

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if not s or not t:
            return ""
        
        # Initialize the character count for t
        target_count = Counter(t)

        # Initialize the character count for the current window in s
        window_count = defaultdict(int)

        # Variables to keep track of the minimum window substring
        min_window_length = float('inf')
        min_window_start = 0

        # Variables for the sliding window
        left_pointer = 0
        right_pointer = 0

        # Number of unique characters in t that need to be present in the window
        required_unique_chars = len(target_count)
        # Number of unique characters in t that are currently present in the window in the required amount
        formed_unique_chars = 0

        # Expand the window by moving the right pointer
        while right_pointer < len(s):
            current_char = s[right_pointer]
            window_count[current_char] += 1

            # Check if the current character is part of t and is present in the required amount in the window
            if current_char in target_count and window_count[current_char] == target_count[current_char]:
                formed_unique_chars += 1

            # Contract the window by moving the left pointer
            while left_pointer <= right_pointer and formed_unique_chars == required_unique_chars:
                # Update the minimum window if the current window is smaller
                window_length = right_pointer - left_pointer + 1
                if window_length < min_window_length:
                    min_window_length = window_length
                    min_window_start = left_pointer

                # Remove the character going out of the window
                char_to_remove = s[left_pointer]
                window_count[char_to_remove] -= 1
                if char_to_remove in target_count and window_count[char_to_remove] < target_count[char_to_remove]:
                    formed_unique_chars -= 1
                left_pointer += 1

            right_pointer += 1

        if min_window_length != float('inf'):
                # If we found a valid window, return the substring from min_window_start with length min_window_length
            return s[min_window_start:min_window_start + min_window_length]
        else:
            # If no valid window was found, return an empty string
            return ""
```

## Thoughts

Got the logic on solving the code in first attempt but actually implementing it took way to long , especially with clearing all the edgecases

Time complexity = O(m+n)  ; sliding window solution on the length of each of the string

Space complexity = O(m+n) ; storage of character counts
