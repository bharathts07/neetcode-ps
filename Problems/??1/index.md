# ??1 String Encode and Decode

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement encode and decode

Example 1:

Input: ["neet","code","love","you"]

Output:["neet","code","love","you"]
Example 2:

Input: ["we","say",":","yes"]

Output: ["we","say",":","yes"]

## Constraints

0 <= strs.length < 100
0 <= strs[i].length < 200
strs[i] contains only UTF-8 characters.

## Solution

```python

class Solution:

    def encode(self, strs: List[str]) -> str:
        res = ""
        for s in strs:
            res = += str(len(s)) + ";" + s
        return res

    def decode(self, s: str) -> List[str]:
        res,i = [], 0

        while i < len(str):
            j = i
            while str[j] != ";"
                j += 1
            length = int(str[i:j])
            res.append(str[j+1:j+1+length])
            i = j + 1 + length
        return res

```

## Thoughts

At first, didn't really understand what was being asked. Since the input and output seeems the same. Then realized that before we product the output we are going through two functions, encode and decode. There is an intermediate steps where we have the words separated by some kind of delimiter.

Actually had to lookup the youtube video to get an idea what to do, but the expkanation is pretty simple. Seems like a pointless exercise. The time and space complexity are both O(n).
