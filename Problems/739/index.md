# [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

**Input:** temperatures = [73,74,75,71,69,72,76,73]
**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**

**Input:** temperatures = [30,40,50,60]
**Output:** [1,1,1,0]

**Example 3:**

**Input:** temperatures = [30,60,90]
**Output:** [1,1,0]

## **Constraints:**

- `1 <= temperatures.length <= 105`
- `30 <= temperatures[i] <= 100`

## Solution

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        # Initialize the result array with zeros
        result = [0] * len(temperatures)
        # Stack to keep track of the indices of temperatures
        stack = []

        for i, temp in enumerate(temperatures):
            # Pop indices from the stack as long as the current temperature is warmer
            # than the temperatures at those indices
            while stack and temperatures[stack[-1]] < temp:
                prev_index = stack.pop()
                result[prev_index] = i - prev_index
            # Push the current index onto the stack
            stack.append(i)

        return result

```

## Thoughts

Initially thought of O(n^2) where you check each element with all remaining elements to get the solution, but using stacks we can reduce it to O(N) solution. ( both in time and space complexity)
