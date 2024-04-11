# [Foreign Dictionary](https://neetcode.io/problems/foreign-dictionary)

There is a foreign language language which uses the latin alphabet, but the order among letters is *not* "a", "b", "c" ... "z" as in English.

You receive a list of *non-empty* strings `words` from the dictionary, where the words are **sorted lexicographically** based on the rules of this new language.

Derive the order of letters in this language. If the order is invalid, return an empty string. If there are multiple valid order of letters, return **any** of them.

A string `a` is lexicographically smaller than a string `b` if either of the following is true:

- The first letter where they differ is smaller in `a` than in `b`.
- There is no index `i` such that `a[i] != b[i]` *and* `a.length < b.length`.

**Example 1:**

```java
Input: ["z","o"]

Output: "zo"
```

Explanation:
From "z" and "o", we know 'z' < 'o', so return "zo".

**Example 2:**

```java
Input: ["hrn","hrf","er","enn","rfnn"]

Output: "hernf"
```

Explanation:

- from "hrn" and "hrf", we know 'n' < 'f'
- from "hrf" and "er", we know 'h' < 'e'
- from "er" and "enn", we know get 'r' < 'n'
- from "enn" and "rfnn" we know 'e'<'r'
- so one possibile solution is "hernf"

## **Constraints:**

- The input `words` will contain characters only from lowercase `'a'` to `'z'`.
- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`

## Solution

```python
from collections import defaultdict, deque

class Solution:
    def foreignDictionary(self, words: List[str]) -> str:
        # Build the graph
        graph = defaultdict(set)
        indegree = {}
        for word in words:
            for c in word:
                if c not in indegree:
                    indegree[c] = 0

        for i in range(len(words) - 1):
            w1, w2 = words[i], words[i + 1]
            min_length = min(len(w1), len(w2))
            for j in range(min_length):
                if w1[j] != w2[j]:
                    # Found the first differing character, add an edge and break
                    if w2[j] not in graph[w1[j]]:
                        graph[w1[j]].add(w2[j])
                        indegree[w2[j]] += 1
                    break
            else:  # This else corresponds to the for loop
                # No break occurred, meaning one word is a prefix of the other
                if len(w1) > len(w2):  # Invalid order if the longer word is first
                    return ""

        # Topological sort using Kahn's algorithm
        start_nodes = deque()
        for c in indegree:
            if indegree[c] == 0:
                start_nodes.append(c)

        order = []
        while start_nodes:
            c = start_nodes.popleft()
            order.append(c)
            for neighbor in graph[c]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    start_nodes.append(neighbor)

        if len(order) == len(indegree):
            return "".join(order)
        else:
            return ""

```

## Thoughts

The else in the section of the code at the indent of for loop, corresponds to the for loop that iterates over the characters of the words w1 and w2. In Python, an else clause can be associated not only with an if statement but also with loops (for and while). When used with a loop, the else block is executed when the loop completes normally (i.e., it is not terminated by a break statement).

In this particular case, the else block is executed when the loop finishes iterating through all the characters in the shorter of the two words (w1 and w2) without encountering a break. This situation arises when one word is a prefix of the other. The if len(w1) > len(w2): check inside the else block is to ensure that the order is valid. If the longer word comes before the shorter word in the list, it is impossible to determine a valid character order, so the function returns an empty string.

### Time Complexity

The time complexity is O(V + E), where V is the number of unique characters in words, and E is the number of edges in the graph. In the worst case, E is O(N), where N is the total number of characters in words.

### Space Complexity

The space complexity is O(V + E) for storing the graph and the indegree map.
