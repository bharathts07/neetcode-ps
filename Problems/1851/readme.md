# [1851. Minimum Interval to Include Each Query](https://leetcode.com/problems/minimum-interval-to-include-each-query/)

You are given a 2D integer array `intervals`, where `intervals[i] = [lefti, righti]` describes the `ith` interval starting at `lefti` and ending at `righti` **(inclusive)**. The **size** of an interval is defined as the number of integers it contains, or more formally `righti - lefti + 1`.

You are also given an integer array `queries`. The answer to the `jth` query is the **size of the smallest interval** `i` such that `lefti <= queries[j] <= righti`. If no such interval exists, the answer is `-1`.

Return *an array containing the answers to the queries*.

**Example 1:**

**Input:** intervals = [[1,4],[2,4],[3,6],[4,4]], queries = [2,3,4,5]
**Output:** [3,3,1,4]
**Explanation:** The queries are processed as follows:

- Query = 2: The interval [2,4] is the smallest interval containing 2. The answer is 4 - 2 + 1 = 3.
- Query = 3: The interval [2,4] is the smallest interval containing 3. The answer is 4 - 2 + 1 = 3.
- Query = 4: The interval [4,4] is the smallest interval containing 4. The answer is 4 - 4 + 1 = 1.
- Query = 5: The interval [3,6] is the smallest interval containing 5. The answer is 6 - 3 + 1 = 4.

**Example 2:**

**Input:** intervals = [[2,3],[2,5],[1,8],[20,25]], queries = [2,19,5,22]
**Output:** [2,-1,4,6]
**Explanation:** The queries are processed as follows:

- Query = 2: The interval [2,3] is the smallest interval containing 2. The answer is 3 - 2 + 1 = 2.
- Query = 19: None of the intervals contain 19. The answer is -1.
- Query = 5: The interval [2,5] is the smallest interval containing 5. The answer is 5 - 2 + 1 = 4.
- Query = 22: The interval [20,25] is the smallest interval containing 22. The answer is 25 - 20 + 1 = 6.

## **Constraints:**

- `1 <= intervals.length <= 105`
- `1 <= queries.length <= 105`
- `intervals[i].length == 2`
- `1 <= lefti <= righti <= 107`
- `1 <= queries[j] <= 107`

## Solution

```python
import heapq

class Solution:
    def minInterval(self, intervals: List[List[int]], queries: List[int]) -> List[int]:
        # Sort intervals by starting point
        intervals.sort()
        # Prepare queries to keep track of original indices
        sorted_queries = sorted((q, i) for i, q in enumerate(queries))

        # Result array and heap initialization
        result = [-1] * len(queries)
        heap = []
        # Pointer to intervals
        interval_idx = 0

        # Process each query in sorted order
        for query_value, query_idx in sorted_queries:
            # Push all intervals that start <= query_value into the heap
            while interval_idx < len(intervals) and intervals[interval_idx][0] <= query_value:
                start, end = intervals[interval_idx]
                heapq.heappush(heap, (end - start + 1, end))
                interval_idx += 1

            # Remove all intervals from the heap that end before the query value
            while heap and heap[0][1] < query_value:
                heapq.heappop(heap)

            # The smallest interval containing the query is at the root of the heap
            if heap:
                result[query_idx] = heap[0][0]

        return result

```

## Thoughts

A really hard problem that requires a lot of thinking. wont be able to do it in interview. But review anyway.

### Time Complexity

O((n+m)logn), where n is the number of intervals and m is the number of queries. This is because we sort the intervals and queries, and then we potentially push and pop each interval into/from the heap.

### Space Complexity

O(n+m) because we store all intervals and the result for each query. The heap can also store up to n intervals in the worst case.
