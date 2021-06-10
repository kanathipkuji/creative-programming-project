# Populating Next Right Pointers in Each Node
https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

## Solution: Breadth First Traversal
### Language: C++

Breadth first traversal traverses nodes level by level. Thus, if we traverse nodes on each level from right to left, we can store previous (right) nodes on the same level.

```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if (root == nullptr) {
            return root;
        }
        queue<Node*> q;
        q.push(root);
        int sz;
        Node *prev, *cur;
        while (!q.empty()) {
            sz = q.size();
            prev = nullptr;
            while (sz--) {
                cur = q.front();
                q.pop();
                cur->next = prev;
                prev = cur;
                
                if (cur->right) {
                    q.push(cur->right);
                }
                if (cur->left) {                
                    q.push(cur->left);
                }
            }
        }
        return root;
    }
};
```

