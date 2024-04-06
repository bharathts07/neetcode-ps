# [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

Given the `root` of a binary tree, return *the length of the **diameter** of the tree*.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]
**Output:** 3
**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3].

**Example 2:**

**Input:** root = [1,2]
**Output:** 1

## **Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-100 <= Node.val <= 100`

## Solution

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        max_diameter = [0]  # Using a list to allow modification within the nested function

        def depth(node, max_diameter):
            if not node:
                return 0

            left_depth = depth(node.left, max_diameter)
            right_depth = depth(node.right, max_diameter)

            # Update the maximum diameter
            max_diameter[0] = max(max_diameter[0], left_depth + right_depth)

            return 1 + max(left_depth, right_depth)

        depth(root, max_diameter)
        return max_diameter[0]

```

## Thoughts

### Time Complexity

The time complexity is O(n), where n is the number of nodes in the tree. This is because we visit each node exactly once in the recursive traversal.

### Space Complexity

The space complexity is O(h), where h is the height of the tree. This is due to the recursive call stack. In the worst case, the tree could be linear (i.e., a linked list), in which case the height of the tree would be equal to the number of nodes, leading to a space complexity of O(n).
