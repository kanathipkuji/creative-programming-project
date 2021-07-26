# Binary Tree Zigzag Level Order Traversal
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

## Solution: Reversing an array every other level
### Language: C++

The code below perform breadth first search where every other level the result list is reversed.

```c++
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (root == nullptr) return vector<vector<int>>();

        queue<pair<TreeNode*, int>> Q;
        Q.emplace(root, 0);

        int lv, prevLv = -1;
        TreeNode* node;
        vector<vector<int>> ret;
        vector<int> V;

        while (!Q.empty()) {
            tie(node, lv) = Q.front();
            Q.pop();
            
            if (prevLv != lv && !V.empty()) {
                if (!(lv & 1)) {
                    reverse(V.begin(), V.end());   
                }
                ret.push_back(V);
                V.clear();
            }
            V.push_back(node->val);
            prevLv = lv;
            if(node->left) Q.emplace(node->left, lv + 1);
            if(node->right) Q.emplace(node->right, lv + 1);
        }
        if (prevLv & 1) {
            reverse(V.begin(), V.end());
        }
        ret.push_back(V);
        return ret;
    }
};
```
