# [207. Course Schedule](https://leetcode.com/problems/course-schedule/)

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

**Input:** numCourses = 2, prerequisites = [[1,0]]
**Output:** true
**Explanation:** There are a total of 2 courses to take.
To take course 1 you should have finished course 0. So it is possible.

**Example 2:**

**Input:** numCourses = 2, prerequisites = [[1,0],[0,1]]
**Output:** false
**Explanation:** There are a total of 2 courses to take.
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

## **Constraints:**

- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs prerequisites[i] are **unique**.

## Solution

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        # Build the graph
        graph = {i: [] for i in range(numCourses)}
        for course, prereq in prerequisites:
            graph[course].append(prereq)

        # Detect cycle using DFS
        visited = [False] * numCourses
        cycle = [False] * numCourses

        def dfs(course):
            if cycle[course]:
                return False
            if visited[course]:
                return True
            visited[course] = True
            cycle[course] = True
            for prereq in graph[course]:
                if not dfs(prereq):
                    return False
            cycle[course] = False
            return True

        for course in range(numCourses):
            if not dfs(course):
                return False
        return True

```

## Thoughts

Review Topological Sort (Kahn's algorithm) later.

### Time Complexity

The time complexity is O(V + E), where V is the number of courses (vertices) and E is the number of prerequisites (edges). This is because we need to visit each node and each edge once in the worst case.

### Space Complexity

The space complexity is O(V + E) for the graph and the visited array. In the worst case, the graph might contain all the courses and prerequisites.
