# [43. Multiply Strings](https://leetcode.com/problems/multiply-strings/)

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

**Note:** You must not use any built-in BigInteger library or convert the inputs to integer directly.

**Example 1:**

**Input:** num1 = "2", num2 = "3"
**Output:** "6"

**Example 2:**

**Input:** num1 = "123", num2 = "456"
**Output:** "56088"

## **Constraints:**

- `1 <= num1.length, num2.length <= 200`
- `num1` and `num2` consist of digits only.
- Both `num1` and `num2` do not contain any leading zero, except the number `0` itself.

## Solution

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == "0" or num2 == "0":
            return "0"

        # Reverse both numbers to simplify the multiplication from least significant digit
        num1, num2 = num1[::-1], num2[::-1]
        n1, n2 = len(num1), len(num2)
        result = [0] * (n1 + n2)  # Maximum length of result can be n1 + n2

        # Multiply each digit and add to the result
        for i in range(n1):
            for j in range(n2):
                # Multiply the current digits
                product = int(num1[i]) * int(num2[j])
                # Place the product at the correct index and add to existing value
                position = i + j
                result[position] += product
                # Handle carry over to the next digit
                result[position + 1] += result[position] // 10
                result[position] %= 10

        # The result list is in reverse order now, so reverse it back
        # Remove leading zeros from the result
        while len(result) > 1 and result[-1] == 0:
            result.pop()

        # Convert list of digits to a string
        result = result[::-1]
        return ''.join(map(str, result))

```

## Thoughts

### Time Complexity

The time complexity is O(N×M), where N and M are the lengths of the two strings. This is due to the nested loops that multiply each digit of num1 by each digit of num2.

### Space Complexity

The space complexity is O(N+M) for the result array that holds up to N+M digits.
