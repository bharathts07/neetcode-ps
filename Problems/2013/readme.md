# [2013. Detect Squares](https://leetcode.com/problems/detect-squares/)

You are given a stream of points on the X-Y plane. Design an algorithm that:

- **Adds** new points from the stream into a data structure. **Duplicate** points are allowed and should be treated as different points.
- Given a query point, **counts** the number of ways to choose three points from the data structure such that the three points and the query point form an **axis-aligned square** with **positive area**.

An **axis-aligned square** is a square whose edges are all the same length and are either parallel or perpendicular to the x-axis and y-axis.

Implement the `DetectSquares` class:

- `DetectSquares()` Initializes the object with an empty data structure.
- `void add(int[] point)` Adds a new point `point = [x, y]` to the data structure.
- `int count(int[] point)` Counts the number of ways to form **axis-aligned squares** with point `point = [x, y]` as described above.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/09/01/image.png)

**Input**
["DetectSquares", "add", "add", "add", "count", "count", "add", "count"]
[[], [[3, 10]], [[11, 2]], [[3, 2]], [[11, 10]], [[14, 8]], [[11, 2]], [[11, 10]]]
**Output**
[null, null, null, null, 1, 0, null, 2]

**Explanation**
DetectSquares detectSquares = new DetectSquares();
detectSquares.add([3, 10]);
detectSquares.add([11, 2]);
detectSquares.add([3, 2]);
detectSquares.count([11, 10]); // return 1. You can choose:
// - The first, second, and third points
detectSquares.count([14, 8]); // return 0. The query point cannot form a square with any points in the data structure.
detectSquares.add([11, 2]); // Adding duplicate points is allowed.
detectSquares.count([11, 10]); // return 2. You can choose:
// - The first, second, and third points
// - The first, third, and fourth points

## **Constraints:**

- `point.length == 2`
- `0 <= x, y <= 1000`
- At most `3000` calls **in total** will be made to `add` and `count`.

## Solution

```python
class DetectSquares:
    def __init__(self):
        from collections import defaultdict
        self.point_count = defaultdict(int)
        self.coord_map = defaultdict(list)

    def add(self, point):
        x, y = point
        self.point_count[(x, y)] += 1
        if y not in self.coord_map[x]:
            self.coord_map[x].append(y)

    def count(self, point):
        x1, y1 = point
        result = 0
        # Check for possible square formations using the horizontal distances
        if x1 in self.coord_map:
            for y2 in self.coord_map[x1]:
                if y2 != y1:
                    side = abs(y2 - y1)
                    # For each potential square side, check corresponding opposite points
                    if (x1 + side, y1) in self.point_count and (x1 + side, y2) in self.point_count:
                        result += self.point_count[(x1 + side, y1)] * self.point_count[(x1, y2)] * self.point_count[(x1 + side, y2)]
                    if (x1 - side, y1) in self.point_count and (x1 - side, y2) in self.point_count:
                        result += self.point_count[(x1 - side, y1)] * self.point_count[(x1, y2)] * self.point_count[(x1 - side, y2)]
        return result



# Your DetectSquares object will be instantiated and called as such:
# obj = DetectSquares()
# obj.add(point)
# param_2 = obj.count(point)
```

## Thoughts

Very confusing, gave up midway, looked at the solution. Definitely needs review

### Time Complexity

O(P), where P represents the total number of unique point entries

### Space Complexity

O(1) for add
O(k^2) in the worst case for each call, where k is the number of different y-coordinates that share the same x-coordinate in the worst case.
