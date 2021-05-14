# Add Two Numbers
https://leetcode.com/problemset/top-interview-questions/

## Solution: Bitmask
### Language: C++

Create two pointers to the same node. One pointer stays at the root of the linked list, and the other traverses through the list.

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *node = new ListNode();
        auto root = node;
        bool first = true;
        int sum, carry = 0;
        while (l1 || l2) {
            sum = carry;
            if (l1) {
                sum += l1->val;
                l1 = l1->next;
            }
            if (l2) {
                sum += l2->val;
                l2 = l2->next;
            }
            carry = sum >= 10;
            node->next = new ListNode(sum % 10);
            node = node->next;
        }
        if (carry) {
            node->next = new ListNode(1);
        }
        if (root == nullptr) {
            return nullptr;
        }
        return root->next;
    }
};       
```
