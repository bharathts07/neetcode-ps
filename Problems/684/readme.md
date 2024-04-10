# [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)

In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two **different** vertices chosen from `1` to `n`, and was not an edge that already existed. The graph is represented as an array `edges` of length `n` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the graph.

Return *an edge that can be removed so that the resulting graph is a tree of* `n` *nodes*. If there are multiple answers, return the answer that occurs last in the input.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-1-graph.jpg)

**Input:** edges = [[1,2],[1,3],[2,3]]
**Output:** [2,3]

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-2-graph.jpg)

**Input:** edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]
**Output:** [1,4]

## **Constraints:**

- `n == edges.length`
- `3 <= n <= 1000`
- `edges[i].length == 2`
- `1 <= ai < bi <= edges.length`
- `ai != bi`
- There are no repeated edges.
- The given graph is connected.

## Solution

```python
class UnionFind:
    def __init__(self, size):
        self.parent = [i for i in range(size + 1)]
        self.rank = [0] * (size + 1)

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            if self.rank[rootX] > self.rank[rootY]:
                self.parent[rootY] = rootX
            elif self.rank[rootX] < self.rank[rootY]:
                self.parent[rootX] = rootY
            else:
                self.parent[rootY] = rootX
                self.rank[rootX] += 1
            return True
        return False

class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        n = len(edges)
        uf = UnionFind(n)
        for a, b in edges:
            if not uf.union(a, b):
                return [a, b]


```

## Thoughts

Review Ackermann function

### Time Complexity

The time complexity is O(N * α(N)), where N is the number of edges, and α(N) is the inverse Ackermann function, which grows very slowly and can be considered almost constant for practical purposes. Therefore, the time complexity is nearly O(N).

### Space Complexity

The space complexity is O(N) for the Union-Find data structure.
