# Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists/

## Solution: Two-pass Iteration
### Language: Python 3

We exploit the fact that if two linked lists of length *n* and *m* have a joint node at *k* nodes away from the end of the list, then there are exactly *n + m + k* iterations from the head of either list to the end and back to the head of another, and lastly, to the joint node. 

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        a, b = headA, headB
        
        while a != b:
            a = headB if a == None else a.next
            b = headA if b == None else b.next
        
        return a
```

