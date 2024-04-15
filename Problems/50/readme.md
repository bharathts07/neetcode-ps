# [50. Pow(x, n)](https://leetcode.com/problems/powx-n/)

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `x^n`).

**Example 1:**

**Input:** x = 2.00000, n = 10
**Output:** 1024.00000

**Example 2:**

**Input:** x = 2.10000, n = 3
**Output:** 9.26100

**Example 3:**

**Input:** x = 2.00000, n = -2
**Output:** 0.25000
**Explanation:** 2-2 = 1/22 = 1/4 = 0.25

## **Constraints:**

- `-100.0 < x < 100.0`
- `-2^31 <= n <= 2^31-1`
- `n` is an integer.
- Either `x` is not zero or `n > 0`.
- `-10^4 <= x^n <= 10^4`

## Solution

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        # Helper function to recursively compute power
        def fast_pow(base, exp):
            if exp == 0:
                return 1  # Base case: any number to the power of 0 is 1

            if exp < 0:
                # If exponent is negative, invert the base and make exponent positive
                return fast_pow(1 / base, -exp)

            half = fast_pow(base, exp // 2)

            if exp % 2 == 0:
                return half * half  # If exponent is even, use the square of half-exponent
            else:
                return half * half * base  # If odd, multiply an additional base to the result

        # Call the helper function with initial parameters
        return fast_pow(x, n)
```

Converting to an iterative solution makes this problem faster but still has the same time complexity

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        if n < 0:
            x = 1 / x
            n = -n

        result = 1
        current_product = x
        while n > 0:
            if n % 2 == 1:  # If n is odd, multiply the current product to the result
                result *= current_product
            current_product *= current_product  # Square the base
            n //= 2  # Reduce n by half

        return result

```

## Thoughts

Not exactly tricky, doable but edges cases are difficult

### Time Complexity

O(log n) for the recursion tree / loop

### Space Complexity

O(log n) for the recursion tree
