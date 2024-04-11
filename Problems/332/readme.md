# [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

You are given a list of airline `tickets` where `tickets[i] = [fromi, toi]` represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

- For example, the itinerary `["JFK", "LGA"]` has a smaller lexical order than `["JFK", "LGB"]`.

You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/03/14/itinerary1-graph.jpg)

**Input:** tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
**Output:** ["JFK","MUC","LHR","SFO","SJC"]

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2021/03/14/itinerary2-graph.jpg)

**Input:** tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
**Output:** ["JFK","ATL","JFK","SFO","ATL","SFO"]
**Explanation:** Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"] but it is larger in lexical order.

**Constraints:**

- `1 <= tickets.length <= 300`
- `tickets[i].length == 2`
- `fromi.length == 3`
- `toi.length == 3`
- `fromi` and `toi` consist of uppercase English letters.
- `fromi != toi`

## Solution

```python
from collections import defaultdict

class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        graph = defaultdict(list)

        # Build graph and sort adjacency lists
        for src, dst in sorted(tickets):
            graph[src].append(dst)

        itinerary = []

        def dfs(airport):
            while graph[airport]:
                next_airport = graph[airport].pop(0)  # Remove the edge (ticket)
                dfs(next_airport)
            itinerary.append(airport)

        dfs("JFK")

        return itinerary[::-1]  # Reverse the itinerary

```

## Thoughts

A very difficult problem. Read that this problem can be solved using a variation of the Eulerian path algorithm, specifically Hierholzer's algorithm, which is used to find an Eulerian path in a graph. Review this later

### Time Complexity

The time complexity is O(E log E), where E is the number of edges (tickets) in the graph. The sorting of the adjacency lists takes O(E log E) time, and the DFS traversal takes O(E) time. However, the overall time complexity is dominated by the sorting step.

### Space Complexity

The space complexity is O(V + E), where V is the number of vertices (airports) and E is the number of edges (tickets) in the graph. The graph itself takes O(V + E) space, and the call stack during DFS takes O(V) space in the worst case.
