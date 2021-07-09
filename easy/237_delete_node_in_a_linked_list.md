# Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list/

## Solution: Replacing Value
### Language: Python 3
### Time Complexity: O(1)

Instead of deleting the node, the code below replace the value of the node to be deleted with the value of its next node, and redirect its pointer to the next one.

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```
