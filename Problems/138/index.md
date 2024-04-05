# [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return *the head of the copied linked list*.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

**Input:** head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
**Output:** [[7,null],[13,0],[11,4],[10,2],[1,0]]

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

**Input:** head = [[1,1],[2,1]]
**Output:** [[1,1],[2,1]]

**Example 3:**

**![e3](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

**Input:** head = [[3,null],[3,0],[3,null]]
**Output:** [[3,null],[3,0],[3,null]]

## **Constraints:**

- `0 <= n <= 1000`
- `-10^4 <= Node.val <= 10^4`
- `Node.random` is `null` or is pointing to some node in the linked list.

## Solution

```python
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return None

        # Step 1: Create a copy of each node and insert it right next to the original node
        current = head
        while current:
            copy = Node(current.val, current.next)
            current.next = copy
            current = copy.next

        # Step 2: Set the random pointers for the copied nodes
        current = head
        while current:
            if current.random:
                current.next.random = current.random.next
            current = current.next.next

        # Step 3: Separate the original list and the copied list
        original = head
        copy = head.next
        copy_head = copy
        while original:
            original.next = original.next.next
            copy.next = copy.next.next if copy.next else None
            original = original.next
            copy = copy.next

        return copy_head

```

## Thoughts

Time complexity: O(n), where n is the number of nodes in the linked list. We traverse the list three times: once to create the copies, once to set the random pointers, and once to separate the lists.

Space complexity: O(1), as we don't use any extra space proportional to the number of nodes in the list.
