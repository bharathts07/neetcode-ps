# [1448. Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

Given a binary tree `root`, a node *X* in the tree is named **good** if in the path from root to *X* there are no nodes with a value *greater than* X.

Return the number of **good** nodes in the binary tree.

**Example 1:**

**![e1](https://assets.leetcode.com/uploads/2020/04/02/test_sample_1.png)**

**Input:** root = [3,1,4,3,null,1,5]
**Output:** 4
**Explanation:** Nodes in blue are **good**.
Root Node (3) is always a good node.
Node 4 -> (3,4) is the maximum value in the path starting from the root.
Node 5 -> (3,4,5) is the maximum value in the path
Node 3 -> (3,1,3) is the maximum value in the path.

**Example 2:**

**![e2](https://assets.leetcode.com/uploads/2020/04/02/test_sample_2.png)**

**Input:** root = [3,3,null,4,2]
**Output:** 3
**Explanation:** Node 2 -> (3, 3, 2) is not good, because "3" is higher than it.

**Example 3:**

**Input:** root = [1]
**Output:** 1
**Explanation:** Root is considered as **good**.

## **Constraints:**

- The number of nodes in the binary tree is in the range `[1, 10^5]`.
- Each node's value is between `[-10^4, 10^4]`.

## Solution

```python
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        def dfs(node, max_val):
            if not node:
                return 0

            count = 1 if node.val >= max_val else 0
            max_val = max(max_val, node.val)
            count += dfs(node.left, max_val)
            count += dfs(node.right, max_val)
            return count

        return dfs(root, root.val)

```

## Thoughts

### Time Complexity

The time complexity of this solution is O(n), where n is the number of nodes in the tree. We visit each node exactly once.

### Space Complexity

The space complexity of this solution is O(h), where h is the height of the tree. This is because the maximum amount of space utilized by the recursion stack would be equal to the height of the tree. In the worst case, the tree is a linear chain (i.e., each node has only one child), and the height of the tree is O(n). In the best case, the tree is completely balanced, and the height of the tree is O(log n).
