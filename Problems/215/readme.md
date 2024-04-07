# [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Given an integer array `nums` and an integer `k`, return *the* `kth` *largest element in the array*.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2
**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4
**Output:** 4

## **Constraints:**

- `1 <= k <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

## Solution

```python
import heapq

class Solution:
    def findKthLargest(self, nums: list[int], k: int) -> int:
        min_heap = nums[:k]
        heapq.heapify(min_heap)
        for num in nums[k:]:
            if num > min_heap[0]:
                heapq.heapreplace(min_heap, num)
        return min_heap[0]

# Example usage
sol = Solution()
print(sol.findKthLargest([3,2,1,5,6,4], 2))  # Output: 5
print(sol.findKthLargest([3,2,3,1,2,4,5,5,6], 4))  # Output: 4

```

## Thoughts

### Time Complexity

O(n log k), where n is the number of elements in the input array. We insert each element into the min heap, which takes O(log k) time, and we do this for all n elements.

### Space Complexity

O(k) for the min heap.
