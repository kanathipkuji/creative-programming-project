# Lowest Common Ancestor of a Binary Tree
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

## 1st Solution: Recursively solve
### Language: Python3
### Time Complexity: O(n) for every query

The core idea is to return the answer whenever it finds *p* node and *q* node on both children.  

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root: return None
        if root == p:
            return p
        elif root == q:
            return q
        l = self.lowestCommonAncestor(root.left, p, q)
        if l and l != p and l != q:
            return l
        r = self.lowestCommonAncestor(root.right, p, q)
        if r and r != p and r != q:
            return r
        if not r: return l
        if not l: return r
        return root if l and r else None        
```

## 2nd Solution: Euler Tour and RMQ 
### Language: Python3
### Time Complexity: O(nlogn) preprocess and O(1) on query

First, construct the euler tour of depth-first-search traversal of the tree. (The euler tour store nodes by the combination of pre-order and post-order traversal.)
Next, construct a sparse table storing an index of the minimum element in the range which is defined by the column. The range increases exponentially from column to column. 
Thus, there is *O(logn)* number of columns, and takes *O(nlogn)* overall to construct the table.
However, the query only takes *O(1)* because the column to be compared can be calculated by log2() function.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        euler=[]
        levels=[]
        firstOccurence={}
        
        self.dfs(root, 0, euler, levels, firstOccurence)
        
        n = len(euler)
        m = floor(log2(n)) + 1
        sparseTable = [[0] * m for _ in range(n)]
        
        self.genSparseTable(levels, sparseTable, n, m)
        
        pIdx = firstOccurence[p.val]
        qIdx = firstOccurence[q.val]
        if pIdx > qIdx:
            pIdx, qIdx = qIdx, pIdx
        l = qIdx - pIdx + 1
        k = floor(log2(l))
        if levels[sparseTable[pIdx][k]] < levels[sparseTable[pIdx + l - 2**k][k]]:
            return euler[sparseTable[pIdx][k]]
        else:
            return euler[sparseTable[pIdx + l - 2**k][k]]
            
    
    def dfs(self, node, level, euler, levels, firstOccurence):
            if not node:
                return
            euler.append(node)
            levels.append(level)
            firstOccurence[node.val] = len(euler) - 1
            if node.left:
                self.dfs(node.left, level + 1, euler, levels, firstOccurence)
                euler.append(node)
                levels.append(level)
            if node.right:
                self.dfs(node.right, level + 1, euler, levels, firstOccurence)
                euler.append(node)
                levels.append(level)

    def genSparseTable(self, levels, sparseTable, n, m):
            for i in range(n):
                sparseTable[i][0] = i
            for j in range(1, m):
                for i in range(n - 2**j + 1):
                    if levels[sparseTable[i][j-1]]<levels[sparseTable[i + 2**(j - 1)][j - 1]]:
                        sparseTable[i][j] = sparseTable[i][j - 1]
                    else:
                        sparseTable[i][j] = sparseTable[i + 2**(j - 1)][j - 1]
        
```
