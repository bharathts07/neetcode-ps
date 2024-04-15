# [7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Given a signed 32-bit integer `x`, return `x` *with its digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example 1:**

**Input:** x = 123
**Output:** 321

**Example 2:**

**Input:** x = -123
**Output:** -321

**Example 3:**

**Input:** x = 120
**Output:** 21

## **Constraints:**

- `-2^31 <= x <= 2^31 - 1`

## Solution

```python
class Solution:
    def reverse(self, x: int) -> int:
        INT_MAX = 2**31 - 1  # Maximum positive int for 32-bit signed integer
        INT_MIN = -2**31     # Minimum negative int for 32-bit signed integer

        rev = 0
        while x != 0:
            # Handle the last digit
            digit = x % 10 if x > 0 else x % -10
            # Reduce x
            x = x // 10 if x > 0 else -(-x // 10)

            # Before pushing digit to rev, check for potential overflow
            if rev > INT_MAX // 10 or (rev == INT_MAX // 10 and digit > INT_MAX % 10):
                return 0
            if rev < INT_MIN // 10 or (rev == INT_MIN // 10 and digit < INT_MIN % 10):
                return 0

            rev = rev * 10 + digit

        return rev
```

## Thoughts

I really hate these bit manipulation questions when checkign for edge cases. Review again, many times.

### Time Complexity

O(log(x)): The number of iterations is proportional to the number of digits in x.

### Space Complexity

O(1): The space used does not depend on the input size, as we only use a few additional variables.
