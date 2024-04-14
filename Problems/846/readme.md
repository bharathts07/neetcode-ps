# [846. Hand of Straights](https://leetcode.com/problems/hand-of-straights/)

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `ith` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

**Example 1:**

**Input:** hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
**Output:** true
**Explanation:** Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]

**Example 2:**

**Input:** hand = [1,2,3,4,5], groupSize = 4
**Output:** false
**Explanation:** Alice's hand can not be rearranged into groups of 4.

## **Constraints:**

- `1 <= hand.length <= 10^4`
- `0 <= hand[i] <= 10^9`
- `1 <= groupSize <= hand.length`

**Note:** This question is the same as 1296: [https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/](https://leetcode.com/problems/divide-array-in-sets-of-k-consecutive-numbers/)

## Solution

```python
from collections import Counter

class Solution:
    def isNStraightHand(self, hand: List[int], groupSize: int) -> bool:
        if len(hand) % groupSize != 0:
            return False

        # Count the frequency of each card
        card_count = Counter(hand)

        # Sort the unique cards
        unique_cards = sorted(card_count)

        # Try to form groups starting from the smallest card
        for card in unique_cards:
            if card_count[card] > 0:  # There are still cards to form a group
                count = card_count[card]
                # Try to form a group of groupSize starting from this card
                for i in range(card, card + groupSize):
                    if card_count[i] < count:
                        return False
                    card_count[i] -= count

        return True

```

## Thoughts

### Time Complexity

O(nlogn) due to the sorting step, where n is the number of cards. The subsequent operations involving counting and decrementing values in a hash map are O(k) for each group, and since each card is considered exactly once, this is still efficient.

### Space Complexity

O(n) for the hash map used to store the count of each unique card. In the worst case, this will store as many entries as there are cards if all are unique.
