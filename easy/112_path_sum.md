# Path Sum
https://leetcode.com/problems/path-sum/

## Solution: Depth First Traversal
### Language: Python 3

On each recursion we reduce *targetSum* by the node's value. Next, the tree has a path sum if the reduced *targetSum*  is equal to any leaf node.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: TreeNode, targetSum: int) -> bool:
        if not root: return False
        if not root.left and not root.right and targetSum == root.val:
            return True
        targetSum -= root.val
        return self.hasPathSum(root.left, targetSum) or self.hasPathSum(root.right, targetSum)
```
