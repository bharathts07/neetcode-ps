# [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.

1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

## **Constraints:**

- `1 <= n <= 45`

## Solution

```python
# Solution 1
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n

        # Initialize the base cases
        one_step_before = 2
        two_steps_before = 1

        # Calculate the number of ways for each step
        for _ in range(3, n + 1):
            ways = one_step_before + two_steps_before
            two_steps_before = one_step_before
            one_step_before = ways

        return one_step_before

```

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        def multiply_matrices(a, b):
            c = [[0, 0], [0, 0]]
            for i in range(2):
                for j in range(2):
                    c[i][j] = a[i][0] * b[0][j] + a[i][1] * b[1][j]
            return c

        def matrix_power(matrix, n):
            if n == 1:
                return matrix
            if n % 2 == 0:
                half_power = matrix_power(matrix, n // 2)
                return multiply_matrices(half_power, half_power)
            else:
                half_power = matrix_power(matrix, n // 2)
                return multiply_matrices(multiply_matrices(half_power, half_power), matrix)

        if n <= 2:
            return n

        transformation_matrix = [[1, 1], [1, 0]]
        initial_state = [[1], [0]]

        # Compute the (n-1)th power of the transformation matrix
        powered_matrix = matrix_power(transformation_matrix, n - 1)

        # Multiply the powered matrix with the initial state
        result = multiply_matrices(powered_matrix, initial_state)

        return result[0][0]  # The top left element is the nth Fibonacci number

```

## Thoughts

### Time Complexity

The time complexity is O(n) since we iterate through the steps from 3 to n.

### Space Complexity

The space complexity is O(1) since we only use a constant amount of space to store the number of ways for the previous two steps.
