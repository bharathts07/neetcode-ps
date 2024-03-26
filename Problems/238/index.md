# 238. Product of Array Except Self

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]

Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]

Constraints:

2 <= nums.length <= 10^5
-30 <= nums[i] <= 30
The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

## Solution

```python

class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        # Initialize the output array
        output = [1] * n

        # Calculate prefix products
        prefix_product = 1
        for i in range(n):
            output[i] = prefix_product
            prefix_product *= nums[i]

        # Calculate suffix products and multiply with prefix products
        suffix_product = 1
        for i in range(n - 1, -1, -1):
            output[i] *= suffix_product
            suffix_product *= nums[i]

        return output

```

## Thoughts

I rememeber having solved this pseud DP problem. First inf all the prefix products for each positions in output array. Then starting from reverse find the reverse suffix product and then multiply it with the original prefix product array, to get your required solun array.

Time complexity = O(n) . We are doing 2 passes for the array
Space Complexity = O(1) . we are told that output array doesn't count , which if it did would be O(n)

Seems like my solution isn't exactly the best. Need to revist this. But the solution was accepted.
