# Binary Tree Preorder Traversal
https://leetcode.com/problems/binary-tree-preorder-traversal/

## Solution: Iteraive Solution Using Stack
### Language: Python 3

We can simulate a recursive search by implementing a LIFO stack.

* Note that right node should be pushed to the stack first in order to traverse in a preorder manner.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if not root: return None
        stack = [root]
        ret = []
        while stack:
            u = stack.pop()
            ret.append(u.val)
            if u.right: stack.append(u.right)
            if u.left: stack.append(u.left)
        return ret
```
