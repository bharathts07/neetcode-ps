# [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

Write a function that takes the binary representation of a positive integer and returns the number of set bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

**Example 1:**

**Input:** n = 11

**Output:** 3

**Explanation:**

The input binary string **1011** has a total of three set bits.

**Example 2:**

**Input:** n = 128

**Output:** 1

**Explanation:**

The input binary string **10000000** has a total of one set bit.

**Example 3:**

**Input:** n = 2147483645

**Output:** 30

**Explanation:**

The input binary string **1111111111111111111111111111101** has a total of thirty set bits.

## **Constraints:**

- `1 <= n <= 2^31 - 1`

**Follow up:** If this function is called many times, how would you optimize it?

## Solution

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0
        while n:
            n &= n - 1  # drop the lowest set bit
            count += 1
        return count

```

## Thoughts

### Time Complexity

O(1) on average; although it depends on the number of set bits in n. In the worst case, it can take up to the number of bits in the integer (32 for a standard integer representation in many systems), but typically it will be much less as most bits are zero in usual cases.

### Space Complexity

O(1), as no additional space is used apart from a few variables.
