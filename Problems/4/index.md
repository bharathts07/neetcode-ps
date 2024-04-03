# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)


Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]
**Output:** 2.00000
**Explanation:** merged array = [1,2,3] and median is 2.

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]
**Output:** 2.50000
**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

## **Constraints:**

- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-10^6 <= nums1[i], nums2[i] <= 10^6`

## Solution
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        # Ensure nums1 is the smaller array
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        smaller_array_length = len(nums1)
        larger_array_length = len(nums2)
        total_elements = smaller_array_length + larger_array_length
        half_length = (total_elements + 1) // 2  # Half of the combined length (rounded up)

        # Binary search on the smaller array
        left_index = 0
        right_index = smaller_array_length
        while left_index < right_index:
            smaller_array_mid = (left_index + right_index) // 2
            larger_array_mid = half_length - smaller_array_mid

            # Check if the current partition is valid
            if nums1[smaller_array_mid] < nums2[larger_array_mid - 1]:
                left_index = smaller_array_mid + 1
            else:
                right_index = smaller_array_mid

        # Final partition indices
        partition_smaller_array = left_index
        partition_larger_array = half_length - partition_smaller_array

        # Elements just to the left and right of the partition
        left_max_smaller_array = float('-inf') if partition_smaller_array == 0 else nums1[partition_smaller_array - 1]
        right_min_smaller_array = float('inf') if partition_smaller_array == smaller_array_length else nums1[partition_smaller_array]
        left_max_larger_array = float('-inf') if partition_larger_array == 0 else nums2[partition_larger_array - 1]
        right_min_larger_array = float('inf') if partition_larger_array == larger_array_length else nums2[partition_larger_array]

        # Compute the median
        if total_elements % 2 == 1:
            return max(left_max_smaller_array, left_max_larger_array)
        else:
            return (max(left_max_smaller_array, left_max_larger_array) + min(right_min_smaller_array, right_min_larger_array)) / 2

```
## Thoughts

No way I'm getting this right in an interview, especially with edge cases. Will revise later

The time complexity of this algorithm is O(log(min(m, n))) because the binary search is performed on the smaller array. The space complexity is O(1) as we only use a constant amount of extra space.
