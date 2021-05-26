# Binary Tree Maximum Path Sum
https://leetcode.com/problems/binary-tree-maximum-path-sum/

## 1st Solution: Recursion
### Language: C++

We create a recursive function that returns optimal solution for every node, i.e. maximum sum of the tree path starting from the current node.
Let the value be *f(node)*.
In that case, we can simply write a recursive form as follows.

* *f(node)* = max{0, max{f(node.left), f(node.right)}} + node.val

*f(node)* will contains the maximum sum of the path that starts from node *node*.
Therefore, the maximum path of the tree will be equal to *max{f(node.left) + f(node.right) + node.val, f(node.left) + node.val, f(node.right) + node.val}* 
for all *node* in the tree.

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
    int ans;
    int depth(TreeNode* node) {
        if(node == nullptr)
            return 0;
        int l, r;
        l = depth(node->left);
        r = depth(node->right);
        ans = max(ans, l + r + node->val);
        ans = max(ans, l + node->val);
        ans = max(ans, r + node->val);
        
        int ret = max(0, max(l, r)) + node->val;
        return ret;
    }
public:
    int maxPathSum(TreeNode* root) {
        ans = root->val;
        depth(root);
        return ans;
    }
};
```
