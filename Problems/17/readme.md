# [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![e1](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

**Example 1:**

**Input:** digits = "23"
**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""
**Output:** []

**Example 3:**

**Input:** digits = "2"
**Output:** ["a","b","c"]

## **Constraints:**

- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

## Solution

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []

        phone_map = {
            '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
            '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'
        }

        def backtrack(index: int, path: str) -> None:
            if index == len(digits):
                result.append(path)
                return
            for letter in phone_map[digits[index]]:
                backtrack(index + 1, path + letter)

        result: List[str] = []
        backtrack(0, "")
        return result

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(4^N), where N is the length of the input digits. This is because, in the worst case, each digit can correspond to 4 letters (e.g., digit '7' corresponds to 'pqrs'), leading to 4^N possible combinations.

### Space Complexity

The space complexity is O(N) for the recursion stack, where N is the length of the input digits. In addition, the space required to store the result is not counted towards the space complexity of the algorithm.
