# [763. Partition Labels](https://leetcode.com/problems/partition-labels/)

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return *a list of integers representing the size of these parts*.

**Example 1:**

**Input:** s = "ababcbacadefegdehijhklij"
**Output:** [9,7,8]
**Explanation:**
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

**Example 2:**

**Input:** s = "eccbbbbdec"
**Output:** [10]

## **Constraints:**

- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

## Solution

```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        # Create a map to store the last occurrence of each character
        last_occurrence = {char: idx for idx, char in enumerate(s)}

        # Initialize variables
        partitions = []
        start = 0
        end = 0

        # Iterate over the string to determine the partitions
        for idx, char in enumerate(s):
            # Update the end to the maximum of the current end or the last occurrence of the current character
            end = max(end, last_occurrence[char])

            # If the current index is the end of a partition
            if idx == end:
                # Calculate the size of the partition and add to the result
                partitions.append(end - start + 1)
                # Update start to the next character after the current end
                start = idx + 1

        return partitions

```

## Thoughts

### Time Complexity

O(n), where n is the length of the string s. We traverse the string twice: once to build the last_occurrence map and once to determine the partitions.

### Space Complexity

O(1), since the last_occurrence map contains at most 26 entries (for the 26 letters of the alphabet). The space for the output list does not count towards the space complexity as it is part of the output.
