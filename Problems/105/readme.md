# [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return *the binary tree*.

**Example 1:**

![e1](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
**Output:** [3,9,20,null,null,15,7]

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]
**Output:** [-1]

## **Constraints:**

- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` and `inorder` consist of **unique** values.
- Each value of `inorder` also appears in `preorder`.
- `preorder` is **guaranteed** to be the preorder traversal of the tree.
- `inorder` is **guaranteed** to be the inorder traversal of the tree.

## Solution

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not preorder or not inorder:
            return None

        # The first element of preorder is the root
        root = TreeNode(preorder[0])
        # Find the index of the root in inorder list
        mid = inorder.index(preorder[0])

        # Recursively construct the left and right subtrees
        root.left = self.buildTree(preorder[1:mid+1], inorder[:mid])
        root.right = self.buildTree(preorder[mid+1:], inorder[mid+1:])

        return root

```

## Thoughts

The recursive construction preorder indices are pretty confusing, need to revise.

### Time Complexity

The time complexity of this solution is O(n^2) in the worst case, where n is the number of nodes in the tree. This is because for each node, we are searching for its index in the inorder list, which takes O(n) time. In the best case, if the tree is balanced, the time complexity can be reduced to O(n log n).

### Space Complexity

The space complexity of this solution is O(n), where n is the number of nodes in the tree. This is because we are storing the entire tree in memory. Additionally, the recursion stack will also use space, but its size will be at most the height of the tree, which is O(log n) in the best case (balanced tree) and O(n) in the worst case (skewed tree).
