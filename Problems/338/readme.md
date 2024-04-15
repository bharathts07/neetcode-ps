# [338. Counting Bits](https://leetcode.com/problems/counting-bits/)

Given an integer `n`, return *an array* `ans` *of length* `n + 1` *such that for each* `i` (`0 <= i <= n`)*,* `ans[i]` \*is the **number of\*** `1`**\*'s** in the binary representation of\* `i`.

**Example 1:**

**Input:** n = 2
**Output:** [0,1,1]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10

**Example 2:**

**Input:** n = 5
**Output:** [0,1,1,2,1,2]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101

## **Constraints:**

- `0 <= n <= 105`

**Follow up:**

- It is very easy to come up with a solution with a runtime of `O(n log n)`. Can you do it in linear time `O(n)` and possibly in a single pass?
- Can you do it without using any built-in function (i.e., like `__builtin_popcount` in C++)?

## Solution

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        # Create a list with n+1 elements, initialized to 0
        result = [0] * (n + 1)

        # Loop through each number from 1 to n (inclusive)
        for i in range(1, n + 1):
            # result[i >> 1] gives the number of set bits in i//2
            # (i & 1) checks if i is odd; if odd, add 1 more set bit
            result[i] = result[i >> 1] + (i & 1)

        # Return the list of results
        return result


```

## Thoughts

### Time Complexity

O(n). We compute the number of set bits for each number from 0 to n exactly once.

### Space Complexity

O(n) for the output array.
