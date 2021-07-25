# Construct Binary Tree from Preorder and Inorder Traversal
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

## Solution: Index Mapping
### Language: Python 3

The algorithm is based on divide and conquer technique. Namely, we extract the root node then recursively extract its left and right nodes, respectively, while incrementing the pointer pointing to preorder list.
However, to find whether the next node will be on the left or right side, we node to see if that node appears before or after the current one in inorder list. Hence, we need to map the value of each node to the index according to the inorder list.


```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        
        hashMap = {}
        for i, node in enumerate(inorder):
            hashMap[node] = i
        i = 0    
        def build(l, r):
            nonlocal i
            if l > r: return None
            val = preorder[i]
            node = TreeNode(val)
            i += 1
            node.left = build(l, hashMap[val] - 1)
            node.right = build(hashMap[val] + 1, r)
            return node
        
        return build(0, len(preorder) - 1)
```

