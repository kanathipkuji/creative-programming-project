# Merge k Sorted Lists
https://leetcode.com/problems/merge-k-sorted-lists/

## Solution: Divide and Conquer
### Language: Python 3
### Time Complexity: O(nlogn)

The idea is similar to merge sort: dividing the lists into two sublists, and recursively merge those sublists.

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists: return None
        if len(lists) == 1: return lists[0]
        
        def mergeTwoLists(l, r):
            dummy = p = ListNode()
            while l and r:
                if l.val < r.val:
                    p.next = l
                    l = l.next
                else:
                    p.next = r
                    r = r.next
                p = p.next
            p.next = l or r
            return dummy.next
        
        def merge__(lists):
            if not lists or len(lists) <= 0: return None
            if len(lists) == 1:
                return lists[0]
            mid = len(lists) // 2
            l = merge__(lists[:mid])
            r = merge__(lists[mid:])
            return mergeTwoLists(l, r)
        
        return merge__(lists)
```
