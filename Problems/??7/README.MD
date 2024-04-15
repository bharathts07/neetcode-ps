# [Meeting Schedule II](https://neetcode.io/problems/meeting-schedule-ii)

Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, find the minimum number of days required to schedule all meetings without any conflicts.

**Example 1:**

```java
Input: intervals = [(0,40),(5,10),(15,20)]

Output: 2
```

Explanation:
day1: (0,40)
day2: (5,10),(15,20)

**Example 2:**

```java
Input: intervals = [(4,9)]

Output: 1
```

**Note:**

- (0,8),(8,10) is not considered a conflict at 8

## **Constraints:**

- `0 <= intervals.length <= 100`
- `0 <= intervals[i].start < intervals[i].end <= 1000`

## Solution

```python
"""
Definition of Interval:
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end
"""

class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return 0

        starts = sorted([interval[0] for interval in intervals])
        ends = sorted([interval[1] for interval in intervals])

        rooms = 0
        end_idx = 0

        # Use two pointers to process starts and ends
        for start in starts:
            if start < ends[end_idx]:
                rooms += 1  # Need a new room
            else:
                end_idx += 1  # Reuse a room

        return rooms

```

## Thoughts

### Time Complexity

O(nlogn) due to sorting the starts and ends.

### Space Complexity

O(n) for storing the starts and ends arrays.
