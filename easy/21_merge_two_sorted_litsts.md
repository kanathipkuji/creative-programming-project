# Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/

## Solution: Straightforward Implementation
### Language: Python3

Note that we can entail the node left in l1 or l2 by running node.next = l1 or l2.

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = node = ListNode()
        while l1 and l2:
            if l1.val < l2.val:
                node.next = l1
                l1 = l1.next
            else:
                node.next = l2
                l2 = l2.next
            node = node.next
        node.next = l1 or l2
        return head.next
```

