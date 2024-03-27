# 125. Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

## Constraints

1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.

## Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Get the pure string 
        filtered_s = ""
        for char in s:
            if char.isalnum():
                filtered_s += char.lower()

        # initialize two pointers
        left = 0                  # Initialize left pointer
        right = len(filtered_s) - 1  # Initialize right pointer

        # Check for palindrome
        while left < right:
            if filtered_s[left] != filtered_s[right]:
                return False
            left += 1 
            right -= 1  

        return True
    
```

## Thoughts

simple strightforward solution. But since I didn't know that isalnum() functions existed the code looked more complex initially. USing python functions makes code to much more easier to read

Time and space complexity are both O(n)
