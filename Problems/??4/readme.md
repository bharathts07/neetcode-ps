# [Valid Tree](https://neetcode.io/problems/valid-tree)

Given `n` nodes labeled from `0` to `n - 1` and a list of `undirected` edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

**Example 1:**

```java
Input:
n = 5
edges = [[0, 1], [0, 2], [0, 3], [1, 4]]

Output:
true
```

**Example 2:**

```java
Input:
n = 5
edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]

Output:
false
```

**Note:**

- You can assume that no duplicate edges will appear in edges. Since all edges are `undirected`, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in edges.

## **Constraints:**

- `1 <= n <= 100`
- `0 <= edges.length <= n * (n - 1) / 2`

## Solution

```python
class UnionFind:
    def __init__(self, size):
        self.parent = [i for i in range(size)]
        self.rank = [0] * size

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
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        if len(edges) != n - 1:  # Check for the number of edges
            return False
        uf = UnionFind(n)
        for a, b in edges:
            if not uf.union(a, b):  # Detect cycle
                return False
        return True

```

## Thoughts

Union Find seems very useful for graph problems.

### Time Complexity

The time complexity is O(E \* α(N)), where E is the number of edges, and α(N) is the inverse Ackermann function, which grows very slowly and can be considered almost constant for practical purposes. Therefore, the time complexity is nearly O(E).

### Space Complexity

The space complexity is O(N) for the Union-Find data structure.
