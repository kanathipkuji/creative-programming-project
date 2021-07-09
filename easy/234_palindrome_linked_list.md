# Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list/

## Solution: Linear Solution
### Language: Python 3
### Time Complexity: O(n)

The solution uses fast and slow pointers. The fast pointer traverses twice as fast as the slow one. When the fast one reaches the end of the list, the slow will reach the middle node.

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        fast = head
        slow = head
        rev = None
        while fast and fast.next:
            fast = fast.next.next
            tmp = slow.next
            slow.next = rev
            rev = slow
            slow = tmp
        if fast:
            slow = slow.next
        while rev and rev.val == slow.val:
            rev = rev.next
            slow = slow.next
        return not rev
```

