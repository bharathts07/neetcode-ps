# [66. Plus One](https://leetcode.com/problems/plus-one/)

You are given a **large integer** represented as an integer array `digits`, where each `digits[i]` is the `ith` digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading `0`'s.

Increment the large integer by one and return *the resulting array of digits*.

**Example 1:**

**Input:** digits = [1,2,3]
**Output:** [1,2,4]
**Explanation:** The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].

**Example 2:**

**Input:** digits = [4,3,2,1]
**Output:** [4,3,2,2]
**Explanation:** The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].

**Example 3:**

**Input:** digits = [9]
**Output:** [1,0]
**Explanation:** The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].

## **Constraints:**

- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`
- `digits` does not contain any leading `0`'s.

## Solution

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        # Length of the digits array
        n = len(digits)

        # Loop over the digits array from right to left
        for i in range(n - 1, -1, -1):
            # If the current digit is less than 9, just increment it by 1
            if digits[i] < 9:
                digits[i] += 1
                # Return immediately since no further increments are needed
                return digits

            # If the current digit is 9, it becomes 0 (due to carry over)
            digits[i] = 0

        # If all digits were 9, we would have carried over past the first digit
        # Example: 999 + 1 = 1000, which means we need an extra leading 1
        # Prepend a 1 to the list of digits to accommodate the extra digit
        return [1] + digits


```

## Thoughts

### Time Complexity

O(n), where n is the number of digits in the array. In the worst case, we iterate through all the digits once.

### Space Complexity

O(1) for the operations, but O(n) if we consider the space required to return the result, as we may need to prepend an extra digit to the array in the worst-case scenario (all digits are 9).
