# Binary Tree Level Order Traversal
https://leetcode.com/problems/binary-tree-level-order-traversal/

## Solution: Breadth First Traversal
### Language: C++

Breadth first traversal traverses level by level. Thus, we modify it so that it separates levels of nodes in order to simplify the solution.

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) return {};
        vector<vector<int>> ret;
        queue<TreeNode*> q;
        q.push(root);
        int sz;
        while (!q.empty()) {
            sz = q.size();
            vector<int> cur;
            while (sz--) {
                auto node = q.front();
                q.pop();
                cur.push_back(node->val);
                if (node->left)
                    q.push(node->left);
                if (node->right)
                    q.push(node->right);

            }
            ret.push_back(cur);
        }
        return ret;
    }
};
```

