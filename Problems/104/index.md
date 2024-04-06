# [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** 3

**Example 2:**

**Input:** root = [1,null,2]
**Output:** 2

## **Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `-100 <= Node.val <= 100`

## Solution

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        # Base case: if the node is None, return 0
        if not root:
            return 0

        # Recursively find the maximum depth of the left and right subtrees
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)

        # Return the maximum of the left and right depths plus one for the current node
        return max(left_depth, right_depth) + 1

```

## Thoughts

### Time Complexity

The time complexity is O(n), where n is the number of nodes in the tree. This is because we visit each node exactly once in the recursive traversal.

### Space Complexity

The space complexity is O(h), where h is the height of the tree. This is due to the recursive call stack. In the worst case, the tree could be linear (i.e., a linked list), in which case the height of the tree would be equal to the number of nodes, leading to a space complexity of O(n).
