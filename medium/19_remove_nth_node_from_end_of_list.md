# Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## Solution: DFS + Dummy Node
### Language: Python3

Create a recursive function that returns the number of nodes from the end of the list including itself.
if the number equals *n*, then it is the node to be deleted. However, to delete the node, we need to know its parent node.
Thus, we check if the next node is the node to be deleted, and delete it. 

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        def dfs(node, n):
            if not node:
                return 0
            idx = dfs(node.next, n)
            if idx == n:
                node.next = node.next.next
            return idx + 1
        dummy = ListNode(0, head)
        dfs(dummy, n)
        return dummy.next
```

