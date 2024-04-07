# [1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return *the weight of the last remaining stone*. If there are no stones left, return `0`.

**Example 1:**

**Input:** stones = [2,7,4,1,8,1]
**Output:** 1
**Explanation:**
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.

**Example 2:**

**Input:** stones = [1]
**Output:** 1

## **Constraints:**

- `1 <= stones.length <= 30`
- `1 <= stones[i] <= 1000`

## Solution

```python
class Solution:
    def lastStoneWeight(self, stones: list[int]) -> int:
        # Convert the list into a max heap
        for i in range(len(stones) // 2 - 1, -1, -1):
            self.heapify_down(stones, len(stones), i)

        while len(stones) > 1:
            # Remove the two heaviest stones
            y = self.pop_max(stones)
            x = self.pop_max(stones)

            # If they are not equal, add the difference back to the heap
            if x != y:
                stones.append(y - x)
                self.heapify_up(stones, len(stones) - 1)

        return stones[0] if stones else 0

    def heapify_up(self, arr: list[int], i: int):
        while i > 0 and arr[(i - 1) // 2] < arr[i]:
            arr[i], arr[(i - 1) // 2] = arr[(i - 1) // 2], arr[i]
            i = (i - 1) // 2

    def heapify_down(self, arr: list[int], n: int, i: int):
        largest = i
        left = 2 * i + 1
        right = 2 * i + 2

        if left < n and arr[left] > arr[largest]:
            largest = left
        if right < n and arr[right] > arr[largest]:
            largest = right

        if largest != i:
            arr[i], arr[largest] = arr[largest], arr[i]
            self.heapify_down(arr, n, largest)

    def pop_max(self, arr: list[int]) -> int:
        n = len(arr)
        arr[0], arr[n - 1] = arr[n - 1], arr[0]
        max_val = arr.pop()
        self.heapify_down(arr, len(arr), 0)
        return max_val

# Example usage
sol = Solution()
print(sol.lastStoneWeight([2,7,4,1,8,1]))  # Output: 1


```

## Thoughts

### Time Complexity

Converting the input array into a max heap takes O(n) time.
Each call to pop_max and the subsequent heapify takes O(log n) time.
In the worst case, we perform O(n) such operations.
Overall, the time complexity is O(n log n).

### Space Complexity

The space complexity is O(1), as we are using the input array itself to implement the max heap.
