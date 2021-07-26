# Sort List
https://leetcode.com/problems/sort-list/

## Solution: Iterative Merge Sort
### Language: Python 3
### Time Complexity: O(nlogn)
### Space Complexity: O(1)

To accomplish the O(1) space constraint, recursive solution is not possible. Thus, we have to solve this iteratively. The solution is to merge sort the list. The split() function splits is a function that cuts the list to be of size *step*, while returning next node.

```python3
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def split(self, node, step):
        while node and step > 1:
            node = node.next
            step -= 1
        if not node: return node
        ret = node.next
        node.next = None
        return ret
    
    def merge(self, left, right, out):
        ret = out
        while left and right:
            if left.val > right.val:
                out.next = right
                right = right.next
            else:
                out.next = left
                left = left.next
            out = out.next
        out.next = left if left else right
        while out.next:
            out = out.next
        return out
    
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        sz = 0
        node = head
        while node:
            node = node.next
            sz += 1
        dummy = ListNode(0, head)
        
        step = 1
        while step < sz:
            node = dummy.next
            tail = dummy
            while node:
                left = node
                right = self.split(left, step)
                node = self.split(right, step)
                tail = self.merge(left, right, tail)
            
            step <<= 1
        
        return dummy.next
```

