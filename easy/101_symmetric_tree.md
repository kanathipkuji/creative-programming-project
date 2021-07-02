# Symmetric Tree
https://leetcode.com/problems/symmetric-tree/

## Solution: Recursive Solution
### Language: Python 3

The following code recursively check if the mirror node, its left child and right child are equal or not.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        
        def check(l, r):
            if not l and not r:
                return True
            if not l or not r:
                return False
            return l.val == r.val and check(l.right, r.left) and check(r.left, l.right)
        
        return check(root, root)
```

