# Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/\

## Solution: Boundary Check
### Language: C++

The solution is to check if the value of the current node is in the boundary or not. The boundary is then bounded to be the one not exceeding its parent, when the function is recursively called.
If the value is not in the boundary, then it is not a binary search tree, i.e. return false.
Otherwise, return if both left child node and right child node are BST.

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
    bool isValidBST(TreeNode* root, long long mn=INT_MIN, long long mx=INT_MAX) {
        if (root == nullptr) {
            return true;
        }
        if (root->val > mx || root->val < mn) {
            return false;
        }
        // cout << root->val << ' ' << mn << ' ' << mx << endl;
        return  isValidBST(root->left, mn, (long long)root->val - 1) && isValidBST(root->right, (long long)root->val + 1, mx);
    }
};
```

