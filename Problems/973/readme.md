# [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

**Input:** points = [[1,3],[-2,2]], k = 1
**Output:** [[-2,2]]
**Explanation:**
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].

**Example 2:**

**Input:** points = [[3,3],[5,-1],[-2,4]], k = 2
**Output:** [[3,3],[-2,4]]
**Explanation:** The answer [[-2,4],[3,3]] would also be accepted.

## **Constraints:**

- `1 <= k <= points.length <= 104`
- `-104 <= xi, yi <= 104`

## Solution

```python
import heapq

class Solution:
    def kClosest(self, points: list[list[int]], k: int) -> list[list[int]]:
        heap = []
        for point in points:
            distance = -(point[0] ** 2 + point[1] ** 2)  # Negate to create a max heap
            if len(heap) < k:
                heapq.heappush(heap, (distance, point))
            else:
                heapq.heappushpop(heap, (distance, point))
        return [point for _, point in heap]

```

## Thoughts

Just use libraries instead of writing one yourself.

### Time Complexity

O(n log k), where n is the number of points in the input array. We insert each point into the heap, which takes O(log k) time, and we do this for all n points.

### Space Complexity

O(k) for the max heap, where k is the number of closest points we want to find.
