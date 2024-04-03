# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"
**Output:** true

**Example 2:**

**Input:** s = "()[]{}"
**Output:** true

**Example 3:**

**Input:** s = "(]"
**Output:** false

## **Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

## Solution

```python
class Solution:
    def isValid(self, s: str) -> bool:
        # Dictionary to map open brackets to their corresponding close brackets
        bracket_map = {'(': ')', '{': '}', '[': ']'}
        # Stack to keep track of open brackets
        stack = []

        for char in s:
            if char in bracket_map:
                # If it's an open bracket, push it onto the stack
                stack.append(char)
            else:
                # If it's a close bracket, check if it matches the top of the stack
                if not stack:
                    # If the stack is empty, there is no open bracket to match
                    return False
                top_of_stack = stack.pop()
                if bracket_map[top_of_stack] != char:
                    # If the close bracket does not match the corresponding open bracket
                    return False

        # If the stack is empty, all open brackets have been matched
        if not stack:
            return True
        else:
            return False


```

## Thoughts

The time complexity of this solution is O(n), where n is the length of the string, because we iterate through each character in the string once. The space complexity is O(n) in the worst case, when all characters in the string are open brackets.
