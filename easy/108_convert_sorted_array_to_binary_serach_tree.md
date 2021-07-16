# Convert Sorted Array to Binary Search Tree
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

## Solution: Divide and Conquer
### Language: Python 3
### Time Complexity: O(nlogn)

We greedily select the middle element from the range as the value of current node, the recursively apply the same algorithm to its left and right child nodes.

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        
        def build(l, r):
            if l > r: return None
            mid = l + (r - l) // 2
            node = TreeNode(nums[mid])
            if l == r: return node
            node.left = build(l, mid - 1)
            node.right = build(mid + 1, r)
            return node
            
        return build(0, len(nums) - 1)
        
```

