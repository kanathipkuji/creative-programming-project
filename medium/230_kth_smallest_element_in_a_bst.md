# Kth Smallest Element in a BST
https://leetcode.com/problems/kth-smallest-element-in-a-bst/

## Solution: Solve by Recursion
### Language: C++

The trick is to decrement the value of k-th by 1 every time we traverse the tree by inorder traversal.

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
    int kthSmallest(TreeNode* root, int& k) {
        int val = INT_MAX;
        if(root->left)
            val = min(val, kthSmallest(root->left, k));
        --k;
        if(k == 0)
            return root->val;
        if(root->right)
            val = min(val, kthSmallest(root->right, k));
        return val;
    }
};
```

