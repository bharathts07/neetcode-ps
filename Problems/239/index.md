# [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3
**Output:** [3,3,5,5,6,7]
**Explanation:**
|Window position  |              Max |
|---------------|-----|
|[1  3  -1] -3  5  3  6  7  |     **3**|
 |1 [3  -1  -3] 5  3  6  7  |     **3**|
 |1  3 [-1  -3  5] 3  6  7  |     **5**|
 |1  3  -1 [-3  5  3] 6  7  |     **5**|
 |1  3  -1  -3 [5  3  6] 7  |     **6**|
| 1  3  -1  -3  5 [3  6  7] |     **7**|


**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

## **Constraints:**

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

## Solution

```python

from collections import deque

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # Initialize the deque and the result list
        deq = deque()
        result = []

        for i in range(len(nums)):
            # Remove indices of elements not in the current window
            while deq and deq[0] < i - k + 1:
                deq.popleft()

            # Remove indices of elements smaller than the current element
            # as they will not be the maximum in this window or any future window
            while deq and nums[deq[-1]] < nums[i]:
                deq.pop()

            # Add the index of the current element
            deq.append(i)

            # The front of the deque is the index of the maximum element in the current window
            if i >= k - 1:
                result.append(nums[deq[0]])

        return result

```

## Thoughts

Python deque and all the functions that it has makes this much easier

Time complexity : O(n) - input array
Space Complexity : O(k) - queue
