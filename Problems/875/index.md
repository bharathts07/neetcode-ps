# [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return *the minimum integer* `k` *such that she can eat all the bananas within* `h` *hours*.

**Example 1:**

**Input:** piles = [3,6,7,11], h = 8
**Output:** 4

**Example 2:**

**Input:** piles = [30,11,23,4,20], h = 5
**Output:** 30

**Example 3:**

**Input:** piles = [30,11,23,4,20], h = 6
**Output:** 23

## **Constraints**

- `1 <= piles.length <= 104`
- `piles.length <= h <= 109`
- `1 <= piles[i] <= 109`

## Solution

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        # Function to calculate total hours taken to eat all bananas at speed k

        def hours_to_eat(k):
            total_hours = 0
            for pile in piles:
                full_hours = pile // k

                remaining_bananas = pile % k
                extra_hour = 1 if remaining_bananas > 0 else 0

                hours_for_pile = full_hours + extra_hour

                total_hours += hours_for_pile

            return total_hours

        # Binary search to find the minimum k
        left, right = 1, max(piles)
        while left < right:
            mid = (left + right) // 2
            if hours_to_eat(mid) <= h:
                right = mid
            else:
                left = mid + 1

        return left

```

## Thoughts

**Time Complexity Analysis:**

- The time complexity is O(n log m), where `n` is the number of piles and `m` is the maximum number of bananas in a pile.
- This is because the `hours_to_eat` function takes O(n) time to compute the total hours for a given `k`, and the binary search over the range `[1, m]` takes O(log m) steps.

**Space Complexity Analysis:**

- The space complexity is O(1) since we are using only a constant amount of additional space for variables `left`, `right`, and `mid`.
