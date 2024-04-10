# [Count Connected Components](https://neetcode.io/problems/count-connected-components)

There is an undirected graph with `n` nodes. There is also an `edges` array, where `edges[i] = [a, b]` means that there is an edge between node `a` and node `b` in the graph.

Return the total number of connected components in that graph.

**Example 1:**

```java
Input:
n=3
edges=[[0,1], [0,2]]

Output:
1
```

**Example 2:**

```java
Input:
n=6
edges=[[0,1], [1,2], [2,3], [4,5]]

Output:
2
```

## **Constraints:**

- `1 <= n <= 100`
- `0 <= edges.length <= n * (n - 1) / 2`

## Solution

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        graph = {i: [] for i in range(n)}
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)

        visited = set()
        def dfs(node):
            if node in visited:
                return
            visited.add(node)
            for neighbor in graph[node]:
                dfs(neighbor)

        count = 0
        for node in range(n):
            if node not in visited:
                count += 1
                dfs(node)

        return count

```

Solution 2 ( union find )

```python
class UnionFind:

    def __init__(self):
        self.f = {}

    def findParent(self, x: int) -> int:
        y = self.f.get(x, x)
        if x != y:
            y = self.f[x] = self.findParent(y)
        return y

    def union(self, x: int, y: int):

        self.f[self.findParent(x)] = self.findParent(y)

class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        dsu = UnionFind()
        for a, b in edges:
            dsu.union(a, b)
        return len(set(dsu.findParent(x) for x in range(n)))

```

## Thoughts

Review union find algorithm. For free problem try leetcode problem 547.

### Time Complexity

The time complexity is O(V + E), where V is the number of nodes and E is the number of edges in the graph. This is because we need to visit each node and each edge once in the worst case.

### Space Complexity

The space complexity is O(V + E) for the graph and the visited set. In the worst case, the graph might contain all the nodes and edges.
