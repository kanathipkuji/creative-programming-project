# Find the Duplicate Number
https://leetcode.com/problems/find-the-duplicate-number/

## Solution: Manipulation on List
### Language: C++
### Time Complexity: O(nlogn)

We create two pointers: *even* and *odd* to create a linked list at even and odd indices, respectively.

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head == nullptr) return head;
        ListNode* odd = head;
        ListNode* even = head->next;
        ListNode* latter = even;
        while(even != nullptr) {
            odd->next = even->next;
            if(odd->next == nullptr) break;            
            odd = odd->next;
            even->next = odd->next;
            even = even->next;
        }
        odd->next = latter;
        while(latter != nullptr) {
            cout << latter->val;
            latter = latter->next;
        }
        return head;
    }
};
```
