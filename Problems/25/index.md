# [25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return *the modified list*.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2

**Output:** [2,1,4,3,5]

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3

**Output:** [3,2,1,4,5]

## **Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 5000`
- `0 <= Node.val <= 1000`

**Follow-up:** Can you solve the problem in `O(1)` extra memory space?

## Solution

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # Helper function to reverse a linked list
        def reverse(head, k):
            prev, curr = None, head
            for _ in range(k):
                nxt = curr.next
                curr.next = prev
                prev = curr
                curr = nxt
            return prev

        # Check if there are at least k nodes left in the list
        count = 0
        curr = head
        while curr and count < k:
            curr = curr.next
            count += 1

        # If there are at least k nodes, reverse them
        if count == k:
            # Reverse the first k nodes
            new_head = reverse(head, k)
            # Recursively reverse the rest of the list and connect it to the first part
            head.next = self.reverseKGroup(curr, k)
            return new_head
        else:
            # If there are less than k nodes left, do not reverse them
            return head

```

## Thoughts

### Time Complexity

The time complexity is O(n), where n is the number of nodes in the list. This is because we traverse each node in the list exactly once.

### Space Complexity

The space complexity is O(n/k) due to the recursive calls. In the worst case, there could be n/k recursive calls, each adding a frame to the call stack.
