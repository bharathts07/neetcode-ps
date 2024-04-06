# [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

Given the `root` of a binary tree, invert the tree, and return *its root*.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

**Input:** root = [4,2,7,1,3,6,9]
**Output:** [4,7,2,9,6,3,1]

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

**Input:** root = [2,1,3]
**Output:** [2,3,1]

**Example 3:**

**Input:** root = []
**Output:** []

## **Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

## Solution

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        # Base case: if the node is null, return null
        if not root:
            return None

        # Recursively invert the left and right subtrees
        left = self.invertTree(root.left)
        right = self.invertTree(root.right)

        # Swap the left and right children
        root.left = right
        root.right = left

        # Return the root of the inverted tree
        return root

```

## Thoughts

### Time Complexity

The time complexity is O(n), where n is the number of nodes in the tree. This is because we visit each node exactly once.

### Space Complexity

The space complexity is O(h), where h is the height of the tree. This is due to the recursive call stack. In the worst case, the tree could be linear (i.e., a linked list), in which case the height of the tree would be equal to the number of nodes, leading to a space complexity of O(n).
