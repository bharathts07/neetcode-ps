# [371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)

Given two integers `a` and `b`, return *the sum of the two integers without using the operators* `+` *and* `-`.

**Example 1:**

**Input:** a = 1, b = 2
**Output:** 3

**Example 2:**

**Input:** a = 2, b = 3
**Output:** 5

**Constraints:**

- `-1000 <= a, b <= 1000`

## Solution

```python
class Solution:
    def getSum(self, a: int, b: int) -> int:
        # mask to handle negative numbers in Python due to infinite bit length
        mask = 0xFFFFFFFF

        while b != 0:
            # compute the sum without carrying
            xor = (a ^ b) & mask

            # compute the carry, and shift left by 1
            carry = ((a & b) << 1) & mask

            # update a and b
            a = xor
            b = carry

        # handle negative results
        if a > 0x7FFFFFFF:
            return ~(a ^ mask)
        return a

```

## Java solution

```java
class Solution {
    public int getSum(int a, int b){
        while(b!=0){
            int tmp = (a & b) << 1 ;
            a = a ^ b;
            b = tmp;
        }
        return a
    }
}

```

## Thoughts

### Time Complexity

O(1): Although this depends on the number of bits in the numbers, since the input constraint limits the values of a and b to a fixed range, the maximum number of iterations is constant (related to the number of bits, which is 32 for standard integer representations).

### Space Complexity

O(1): The solution uses only a constant amount of extra space for variables, regardless of the input size.
