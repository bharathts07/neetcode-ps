# [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string `s`, partition `s` such that every substring of the partition is a  **palindrome**

. Return *all possible palindrome partitioning of* `s`.

**Example 1:**

**Input:** s = "aab"
**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"
**Output:** [["a"]]

**Constraints:**

- `1 <= s.length <= 16`
- `s` contains only lowercase English letters.

## Solution

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        def isPalindrome(sub: str) -> bool:
            # easy way to create a reverse of a given string using splices
            return sub == sub[::-1]

        def backtrack(start: int, path: List[str]) -> None:
            if start == len(s):
                result.append(path.copy())
                return
            for end in range(start + 1, len(s) + 1):
                if isPalindrome(s[start:end]):
                    path.append(s[start:end])
                    backtrack(end, path)
                    path.pop()

        result: List[List[str]] = []
        backtrack(0, [])
        return result

```

## Thoughts

Was too sleepy and tool help, need to revisit this again, especially the indices.

### Time Complexity

The time complexity of this solution is O(N \* 2^N), where N is the length of the string. This is because, in the worst case, we might need to check each substring for being a palindrome, which takes O(N) time, and there are 2^N possible partitions.

### Space Complexity

The space complexity is O(N) for the recursion stack. Additionally, the space required to store the result is not counted towards the space complexity of the algorithm.
