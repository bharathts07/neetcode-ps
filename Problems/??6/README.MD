# [Meeting Schedule](https://neetcode.io/problems/meeting-schedule)

Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, determine if a person could add all meetings to their schedule without any conflicts.

**Example 1:**

```java
Input: intervals = [(0,30),(5,10),(15,20)]

Output: false

Explanation:
(0,30),(5,10) and (0,30),(15,20) will conflict
```

**Example 2:**

```java
Input: intervals = [(5,8),(9,15)]

Output: true
```

**Note:**

- (0,8),(8,10) is not considered a conflict at 8

## **Constraints:**

- `0 <= intervals.length <= 100`
- `0 <= intervals[i].start < intervals[i].end <= 1000`

## Solution

```python
class Interval(object):
    def __init__(self, start, end):
        self.start = start
        self.end = end

class Solution:
    def canAttendMeetings(self, intervals: List[Interval]) -> bool:
        # Sort intervals based on the start time
        intervals.sort(key=lambda x: (x.start, x.end))

        # Check for overlaps between consecutive intervals
        for i in range(len(intervals) - 1):
            if intervals[i].end > intervals[i+1].start:
                # There is an overlap, return False
                return False

        # If no overlaps found, return True
        return True

```

## Thoughts

### Time Complexity

O(nlogn) for sorting.

### Space Complexity

O(1) or O(n) depending on the space used by the sorting algorithm.
