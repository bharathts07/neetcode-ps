# [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return *the values of the nodes you can see ordered from top to bottom*.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

**Input:** root = [1,2,3,null,5,null,4]
**Output:** [1,3,4]

**Example 2:**

**Input:** root = [1,null,3]
**Output:** [1,3]

**Example 3:**

**Input:** root = []
**Output:** []

## **Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

## Solution

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root:
            return []

        result = []
        queue = [root]

        while queue:
            level_size = len(queue)
            for i in range(level_size):
                node = queue.pop(0)
                if i == level_size - 1:  # Add the last node of each level
                    result.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return result
```

## Thoughts

### Time Complexity

The time complexity of this solution is O(n), where n is the number of nodes in the tree. We visit each node exactly once.

### Space Complexity

The space complexity of this solution is O(n) in the worst case when the tree is completely unbalanced (e.g., each node has only one child). In the best case (a completely balanced tree), the space complexity would be O(w), where w is the maximum width of the tree.
