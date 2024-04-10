# [127. Word Ladder](https://leetcode.com/problems/word-ladder/)

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return *the **number of words** in the **shortest transformation sequence** from* `beginWord` *to* `endWord`*, or* `0` *if no such sequence exists.*

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
**Output:** 5
**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
**Output:** 0
**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

**Constraints:**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`, `endWord`, and `wordList[i]` consist of lowercase English letters.
- `beginWord != endWord`
- All the words in `wordList` are **unique**.

## Solution

```python
from collections import defaultdict, deque

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList:
            return 0

        # Preprocess the word list to create a dictionary of generic patterns
        word_patterns = defaultdict(list)
        for word in wordList:
            for i in range(len(word)):
                pattern = word[:i] + '*' + word[i + 1:]
                word_patterns[pattern].append(word)

        # BFS
        queue = deque([(beginWord, 1)])
        visited = set([beginWord])
        while queue:
            word, steps = queue.popleft()
            for i in range(len(word)):
                pattern = word[:i] + '*' + word[i + 1:]
                for next_word in word_patterns[pattern]:
                    if next_word == endWord:
                        return steps + 1
                    if next_word not in visited:
                        visited.add(next_word)
                        queue.append((next_word, steps + 1))

        return 0

```

## Thoughts

### Time Complexity

The time complexity is O(N * L^2), where N is the number of words in the word list and L is the length of each word. This is because we generate L patterns for each word and each pattern takes O(L) time to create.

### Space Complexity

The space complexity is O(N * L^2) for the word_patterns dictionary and O(N) for the visited set and the queue.
