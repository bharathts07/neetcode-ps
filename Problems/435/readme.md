# [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping*.

**Example 1:**

**Input:** intervals = [[1,2],[2,3],[3,4],[1,3]]
**Output:** 1
**Explanation:** [1,3] can be removed and the rest of the intervals are non-overlapping.

**Example 2:**

**Input:** intervals = [[1,2],[1,2],[1,2]]
**Output:** 2
**Explanation:** You need to remove two [1,2] to make the rest of the intervals non-overlapping.

**Example 3:**

**Input:** intervals = [[1,2],[2,3]]
**Output:** 0
**Explanation:** You don't need to remove any of the intervals since they're already non-overlapping.

## **Constraints:**

- `1 <= intervals.length <= 10^5`
- `intervals[i].length == 2`
- `-5 * 10^4 <= starti < endi <= 5 * 10^4`

## Solution

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return 0

        # Sort the intervals based on their end values
        intervals.sort(key=lambda x: x[1])

        # Initialize the first interval as non-overlapping
        last_end = intervals[0][1]
        count_non_overlapping = 1  # Count the first interval

        # Iterate through the sorted intervals starting from the second one
        for start, end in intervals[1:]:
            if start >= last_end:
                count_non_overlapping += 1
                last_end = end

        # Total intervals minus the number of non-overlapping intervals gives the number to remove
        return len(intervals) - count_non_overlapping

```

## Thoughts

Sort Intervals by End Time: Sort the intervals by their end times. This allows us to always have a greedy choice of picking the interval that finishes the earliest.

Count Non-overlapping Intervals: Iterate through the sorted intervals and keep track of the end of the last added interval. If the current interval starts after the last added interval, it doesn't overlap, and we can consider it as part of the non-overlapping set. Otherwise, skip this interval (consider it as removed).

### Time Complexity

O(nlogn), where n is the number of intervals. The sorting of intervals takes O(nlogn), and a single pass through the intervals takes O(n). Hence, the overall time complexity is dominated by the sorting step.

### Space Complexity

O(logn) due to the space used by the sorting algorithm, assuming an in-place sort is not used (such as Timsort in Python). If sorting happens in-place, the space complexity can be considered O(1).
