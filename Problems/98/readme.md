# [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left

  subtree

  of a node contains only nodes with keys **less than** the node's key.

- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]
**Output:** true

**Example 2:**

![e2](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]
**Output:** false
**Explanation:** The root node's value is 5 but its right child's value is 4.

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-2^31 <= Node.val <= 2^31 - 1`

## Solution

```python

# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def isValid(node, min_val, max_val):
            if not node:
                return True

            if not (min_val < node.val < max_val):
                return False

            return isValid(node.left, min_val, node.val) and isValid(node.right, node.val, max_val)

        return isValid(root, float('-inf'), float('inf'))

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(n), where n is the number of nodes in the tree. This is because we visit each node exactly once during the traversal.

### Space Complexity

The space complexity of this solution is O(h), where h is the height of the tree. This is because the maximum amount of space utilized by the recursion stack would be equal to the height of the tree. In the worst case, the tree is a linear chain (i.e., each node has only one child), and the height of the tree is O(n). In the best case, the tree is completely balanced, and the height of the tree is O(log n).

Overall, the solution efficiently checks whether a binary tree is a valid binary search tree with linear time complexity and space complexity dependent on the height of the tree.
