# Remove Duplicates from Sorted List
https://leetcode.com/problems/remove-duplicates-from-sorted-list/

## Solution: Simple Iteration
### Language: Python 3

The solution is to iterate through the list while keeping the previous node, which is the node prior to the current one, whose value appears first on the list. 

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head: return head
        prev = head
        cur = head.next
        while cur:
            if cur.val == prev.val:
                prev.next = cur.next
            else: 
                prev = cur
            cur = cur.next
        return head
```

