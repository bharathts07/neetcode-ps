# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3
**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1
**Output:** ["()"]

## **Constraints:**

- `1 <= n <= 8`

## Solution

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []

        def backtrack(combination, open_count, close_count):
            # Base case: if the combination is complete (length is 2 * n), add it to the result
            if len(combination) == 2 * n:
                result.append(combination)
                return
            
            # If we can add more open parentheses (based on n), add '(' and recurse
            if open_count < n:
                backtrack(combination + '(', open_count + 1, close_count)
            
            # If we can add more close parentheses (based on the number of open parentheses), add ')' and recurse
            if close_count < open_count:
                backtrack(combination + ')', open_count, close_count + 1)

        # Start the recursion with an empty combination and counts set to 0
        backtrack('', 0, 0)
        return result

```

## Thoughts

Was able to solve the problem but struggled with determining the time and pace complexity. After researching and asking chatgpt got this response :

The time and space complexity of generating all combinations of well-formed parentheses is closely related to the Catalan numbers, which have many applications in combinatorial mathematics.

**Time Complexity:**

The time complexity of this problem is O(4^n / sqrt(n)). Here's why:

The number of valid combinations of well-formed parentheses for n pairs is the nth Catalan number, which is given by the formula C(n) = (2n)! / ((n + 1)!n!).

This formula grows asymptotically as O(4^n / (n^(3/2))).

For each valid combination, we need to construct a string of length 2n, which takes O(n) time.

Therefore, the overall time complexity is

`O(n * C(n)) = O(n * 4^n / (n^(3/2))) = O(4^n / sqrt(n)).`

**Space Complexity:**

The space complexity of this problem is also O(4^n / sqrt(n)) for the following reasons:

The recursion depth can go up to 2n, as we need to construct strings of length 2n. Therefore, the space used by the system stack is O(2n) = O(n).
The number of valid combinations stored in the result list is the nth Catalan number, which is O(4^n / sqrt(n)).
Each combination is a string of length 2n, but since strings are immutable in Python, each recursive call creates a new string. However, we only need to consider the space for the final combinations in the result list, as the temporary strings created during recursion are not stored simultaneously.
Therefore, the space complexity is dominated by the space needed to store the result list, which is O(4^n / sqrt(n)).

In summary, both the time and space complexity of generating all combinations of well-formed parentheses for n pairs are O(4^n / sqrt(n)), which is exponential due to the nature of the problem.
