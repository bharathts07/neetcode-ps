# [139. Word Break](https://leetcode.com/problems/word-break/)

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]
**Output:** true
**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]
**Output:** true
**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
**Output:** false

## **Constraints:**

- `1 <= s.length <= 300`
- `1 <= wordDict.length <= 1000`
- `1 <= wordDict[i].length <= 20`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of `wordDict` are **unique**.

## Solution

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        word_set = set(wordDict)  # Use a set for O(1) lookup time
        dp = [False] * (len(s) + 1)
        dp[0] = True  # Base case: empty string is "segmentable"

        for i in range(1, len(s) + 1):
            for j in range(i):
                if dp[j] and s[j:i] in word_set:
                    dp[i] = True
                    break  # No need to check further if dp[i] is true

        return dp[len(s)]

```

## Thoughts

### Time Complexity

O(n^2 \* k): Where n is the length of the string s and k is the average length of words in the dictionary.
The nested loop structure gives us O(n^2), since for each i, we potentially check every j less than i.
Checking if a substring s[j:i] exists in the set takes O(k) where k is the length of the substring on average. Given the set lookup itself is O(1), substring creation dominates this part.

### Space Complexity

O(n + m):
O(n) for the dp array.
O(m) for the word_set, where m is the total number of characters in all words in the dictionary if implemented using a set or a trie can optimize it further.
