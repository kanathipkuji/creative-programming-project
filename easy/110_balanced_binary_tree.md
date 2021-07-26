# Balanced Binary Tree
https://leetcode.com/problems/balanced-binary-tree/

## Solution: Depth First Traversal
### Language: Python 3

The code below recursively find the height of the left and right subtrees, and combine it to compute the height starting from the root node. At the same time, if those heights differ by more than 1 node, then mark it as impossible (-1).

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def check(root):
            if not root: return 0
            l = check(root.left)
            r = check(root.right)
            if l == -1 or r == -1 or abs(l - r) > 1:
                return -1
            return max(l, r) + 1
        return check(root) != -1
```
