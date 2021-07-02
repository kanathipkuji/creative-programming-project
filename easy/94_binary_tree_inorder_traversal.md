# Valid Palindrome
https://leetcode.com/problems/valid-palindrome/

## Solution: Recursive Traversal
### Language: Python 3

Inorder traversal can be implemented using a recursive function as shown below.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        ret = []
        
        def dfs(root):
            if not root: return
            if root.left: dfs(root.left)
            ret.append(root.val)
            if root.right: dfs(root.right)
        
        dfs(root)
        
        return ret
```

