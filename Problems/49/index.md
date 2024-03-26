# 49. Group Anagrams

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:

Input: strs = [""]
Output: [[""]]

Example 3:

Input: strs = ["a"]
Output: [["a"]]

## Constraints

1 <= strs.length <= 10^4
0 <= strs[i].length <= 100
strs[i] consists of lowercase English letters.

## Solution

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # Create a dictionary to group anagrams. The key is the sorted form of the word,
        # and the value is a list of words that are anagrams of each other.
        anagrams = {}

        # Iterate through the list of strings.
        for s in strs:
            # Sort the characters in the string to form the key.
            key = tuple(sorted(s))

            # If the key is not in the dictionary, add it with a new list containing the current string.
            # Otherwise, append the current string to the existing list.
            if key not in anagrams:
                anagrams[key] = [s]
            else:
                anagrams[key].append(s)

        # Return the values of the dictionary, which are lists of anagrams.
        return list(anagrams.values())

```

## Thoughts

Seemed pretty hard at first. Got an idea how to solve it in terms of pseudocode but eventually had to use ChatGPT to actually type up the logic in python.

Time complexity is O(n*m)  where n is the number of elements and m is the lemgth of the longest string
Space complexity is again O(m*n)
