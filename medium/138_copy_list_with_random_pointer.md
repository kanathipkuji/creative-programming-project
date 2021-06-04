# Copy List with Random Pointer
https://leetcode.com/problems/copy-list-with-random-pointer/

## 1st Solution: Storing in a hash table
### Language: C++
### Time Complexity: O(n)
### Space Complexity: O(m) where m is the size of the hash table

On each step to locate the pointer of *next* and *random*, we check if the node already existed or not. If it is not, we have to create a new node, and point to that node.

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (head == nullptr) return nullptr;
        unordered_map<Node*, Node*> uset;
        Node* node = new Node(head->val);
        uset[head] = node; 
        auto ret = node;
        while (head) {
            auto it = uset.find(head->random); 
            if (it == uset.end()) {
                if (head->random)
                    node->random = new Node(head->random->val);
                uset[head->random] = node->random;

            } else {
                node->random = it->second;
            }
            
            it = uset.find(head->next);
            if (it == uset.end()) {
                if (head->next)
                    node->next = new Node(head->next->val);
                uset[head->next] = node->next;

            } else {
                node->next = it->second;
            }
            node = node->next;
            head = head->next;
        }
        return ret;
    }
};
```

## 2nd Solution: Storing in a hash table
### Language: C++
### Time Complexity: O(n)
### Space Complexity: O(1)

This approach creates 3 loops with different objectives. 

1. Create new nodes next to nodes in the given list, pointing to node->next of the original one.
2. Assign random pointer to all new nodes.
3. Seperate new nodes and original nodes.

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (head == nullptr) return nullptr;
        Node* it2;
        for (auto it = head; it; it = it->next->next) {
            it2 = it->next;
            it->next = new Node(it->val);
            it->next->next = it2;
        }
        for (auto it = head; it; it = it->next->next) {
            if (it->random)
                it->next->random = it->random->next;
        }
        
        auto ret = head->next;
        for (auto it = head; it; it = it->next) {
            it2 = it->next;
            it->next = it2->next;
            if (it2->next)
                it2->next = it2->next->next;
        }
        return ret;
    }
};
```

