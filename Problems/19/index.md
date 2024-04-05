# [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)


Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2
**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1
**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1
**Output:** [1]

## **Constraints:**

- The number of nodes in the list is `sz`.
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

**Follow up:** Could you do this in one pass?

## Solution

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        # Create a dummy node to handle edge cases such as removing the first node
        dummy = ListNode(0)
        dummy.next = head

        # Initialize two pointers
        first = dummy
        second = dummy

        # Move first pointer so that the gap between first and second is n nodes
        for _ in range(n + 1):
            first = first.next

        # Move first to the end, maintaining the gap
        while first is not None:
            first = first.next
            second = second.next

        # Skip the nth node
        second.next = second.next.next

        # Return the head of the modified list
        return dummy.next

```

## Thoughts

Strightforward soln
O(n) time complexity
O(1) space for temp variables.
