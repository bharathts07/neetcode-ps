# 128. Longest Consecutive Sequence

Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in O(n) time.

Example 1:

Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:

Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9

## Constraints

0 <= nums.length <= 10^5
-10^9 <= nums[i] <= 10^9

## Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        num_set = set(nums)
        longest_streak = 0

        for num in num_set:
            # Check if it's the start of a sequence
            if num - 1 not in num_set:
                current_num = num
                current_streak = 1

                # Count consecutive elements
                while current_num + 1 in num_set:
                    current_num += 1
                    current_streak += 1

                longest_streak = max(longest_streak, current_streak)

        return longest_streak
```

## Thoughts

Initially thought of sorting the list and counting the successive elements at each position. But sorting would take O(nlong) time. Then thought of using set which is said to have O(1) lookup. So now the time and space complexity would be O(n), assuming the set lookup is O(1), it could be O(n^2) if the set has a lot collision in case of large set of numbers.
