# Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/

## Solution: Tortoise and Hare Algorithm
### Language: Python 3

Tortoise and Hare algorithm utilizes 2 pointers: one traverses twice as fast as the other.
As the distance between these 2 pointers increases by 1 for each iteration, if there is a cycle in the list, there must exist one *i* such that on the *i*-th iteration the 2 pointers point to the same node.

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head: return False
        slow = head
        fast = head.next
        while fast and fast.next and slow != fast:
            fast = fast.next.next
            slow = slow.next
        return bool(fast) and bool(fast.next)

```

