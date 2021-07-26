# Binary Tree Postorder Traversal
https://leetcode.com/problems/binary-tree-preorder-traversal/

## Solution: Iteraive Solution Using Stack
### Language: Python 3

The solution is similar to the preorder traversal question, but instead of traversing the left node first, postorder traversal traverses the right one. After all nodes have been traversed, the postorder list is inverted.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        if not root: return None
        stack = [root]
        ret = []
        while stack:
            u = stack.pop()
            ret.append(u.val)
            if u.left: stack.append(u.left)
            if u.right: stack.append(u.right)
        return ret[::-1]
```
