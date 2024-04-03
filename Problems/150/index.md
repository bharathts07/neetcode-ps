# [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

You are given an array of strings `tokens` that represents an arithmetic expression in a [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Evaluate the expression. Return _an integer that represents the value of the expression_.

**Note** that:

- The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers always **truncates toward zero**.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a **32-bit** integer.

**Example 1:**

**Input:** tokens = ["2","1","+","3","*"]
**Output:** 9
**Explanation:** ((2 + 1) * 3) = 9

**Example 2:**

**Input:** tokens = ["4","13","5","/","+"]
**Output:** 6
**Explanation:** (4 + (13 / 5)) = 6

**Example 3:**

**Input:**

`tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]`

**Output:** 22
**Explanation:**
`= ((10 * (6 / ((9 + 3) * -11))) + 17) + 5`
`= ((10 * (6 / (12 * -11))) + 17) + 5`
`= ((10 * (6 / -132)) + 17) + 5`
`= ((10 * 0) + 17) + 5`
`= (0 + 17) + 5`
`= 17 + 5`
`= 22`

## **Constraints:**

- `1 <= tokens.length <= 104`
- `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

## Solution

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for token in tokens:
            if token in '+-*/':
                # Pop the top two operands from the stack
                operand2 = stack.pop()
                operand1 = stack.pop()
                
                # Perform the operation and push the result back onto the stack
                if token == '+':
                    stack.append(operand1 + operand2)
                elif token == '-':
                    stack.append(operand1 - operand2)
                elif token == '*':
                    stack.append(operand1 * operand2)
                elif token == '/':
                    # Division should truncate toward zero
                    stack.append(int(operand1 / operand2))
            else:
                # If the token is an operand, push it onto the stack
                stack.append(int(token))

        # The final result will be the only element left in the stack
        return stack.pop()

```

## Thoughts

The time complexity of this solution is O(n), where n is the number of tokens in the input array, because we iterate through each token once. The space complexity is O(n) in the worst case, when all tokens are operands, and we need to store them in the stack.
