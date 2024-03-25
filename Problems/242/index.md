# 242. Valid Anagram

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: s = "anagram", t = "nagaram"
Output: true

Example 2:

Input: s = "rat", t = "car"
Output: false

## Constraints

1 <= s.length, t.length <= 5 * 10^4
s and t consist of lowercase English letters.

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        # Create a dictionary to count occurrences of each character in s
        char_count = {}
        for char in s:
            if char in char_count:
                char_count[char] += 1
            else:
                char_count[char] = 1

        # Decrease the count for each character in t
        for char in t:
            if char not in char_count or char_count[char] == 0:
                # If a character is not in s or occurs more times in t, return False
                return False
            char_count[char] -= 1

        # If all counts are zero, then t is an anagram of s
        for count in char_count.values():
            if count != 0:
                return False

        return True
```

## Thoughts

Initially thought of sorting the two strings and then comparing the sorted strings. But this would be O(nlog(n)) solution.
Next thought of tries and how characters are kept track along the path for searching using maps.
The above solution would be O(n) time complexity where n is the length of the longest string of s and t and O(K) space complexity since the number of characters are fixed. Having unicode characters still means that we have fixed number of characters (keys for the map)
