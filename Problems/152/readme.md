# [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

Given an integer array `nums`, find a  subarray that has the largest product, and return *the product*.

The test cases are generated so that the answer will fit in a **32-bit** integer.

**Example 1:**

**Input:** nums = [2,3,-2,4]
**Output:** 6
**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]
**Output:** 0
**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

## **Constraints:**

- `1 <= nums.length <= 2 * 104`
- `-10 <= nums[i] <= 10`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if not nums:
            return 0

        max_so_far = min_so_far = global_max = nums[0]

        for i in range(1, len(nums)):
            temp = max_so_far
            max_so_far = max(nums[i], max_so_far * nums[i], min_so_far * nums[i])
            min_so_far = min(nums[i], temp * nums[i], min_so_far * nums[i])
            global_max = max(global_max, max_so_far)

        return global_max
```

## Thoughts

### Time Complexity

O(n): We traverse the array once, updating our running products and global maximum in constant time for each element.

### Space Complexity

O(1): The space usage is constant as we're only using a few variables to keep track of the current maximum and minimum products and the global maximum.
