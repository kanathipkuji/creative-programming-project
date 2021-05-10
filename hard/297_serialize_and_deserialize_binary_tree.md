# Serialize and Deserialize Binary Tree
https://leetcode.com/problems/serialize-and-deserialize-binary-tree/

## Solution: 
### Language: Python3

* 	The approach transforms the binary tree into a list containing its pre-order traversal.
* 	In the deserialize() function, store the index of the serialized data, as a reference value, by wrapping the value with a list.

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root, l=[]):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            l.append('.')
        else:
            l.append(str(root.val))
            self.serialize(root.left, l)
            self.serialize(root.right, l)
        return l

    def deserialize(self, data, idx=[0]):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        cur = data[idx[0]]
        idx[0] += 1
        
        if cur == '.' or not cur:
            return None
        
        root = TreeNode(int(cur))   
        root.left = self.deserialize(data, idx)
        root.right = self.deserialize(data, idx)
        return root
            
            
# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```
