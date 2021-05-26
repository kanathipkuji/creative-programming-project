# Word Search
https://leetcode.com/problems/word-search-ii/

## 1st Solution: Recursion
### Language: Python3
### Time Complexity: O(nlogn)

We create a recursive function that returns optimal solution for every node, i.e. maximum sum of the tree path starting from the current node.
Let the value be *f(node)*.
In that case, we can simply write a recursive form as follows.

* *f(node)* = max{0, max{f(node.left), f(node.right)}} + node.val

*f(node)* will contains the maximum sum of the path that starts from node *node*.
Therefore, the maximum path of the tree will be equal to *max{f(node.left) + f(node.right) + node.val, f(node.left) + node.val, f(node.right) + node.val}* 
for all *node* in the tree.



```c++
class Solution {
    struct TrieNode{
        TrieNode* next[26]{};
        string word;
    };
    
    void buildTrie(string &word, TrieNode* root) {
        for(auto c: word) {
            cout << c-'a' << endl;
            if(root->next[c - 'a'] == nullptr) {
                root->next[c - 'a'] = new TrieNode();
            }
            root = root->next[c - 'a'];
        }
        root->word = word;
    }
    
    void dfs(int x, int y, vector<vector<char>>& board, vector<string>& ret, TrieNode* root) {
        char c = board[x][y];
        if(!isalpha(c) || root->next[c - 'a'] == nullptr)
            return;
        root = root->next[c - 'a'];
        if(root->word != "") {
            ret.push_back(root->word);
            root->word = "";
        }
        board[x][y] = '-';
        if(x > 0)
         dfs(x - 1, y, board, ret, root);
        if(y > 0)
         dfs(x, y - 1, board, ret, root);
        if(x < board.size()-1)
         dfs(x + 1, y, board, ret, root);
        if(y < board[0].size()-1)
         dfs(x, y+1, board, ret, root);
        board[x][y] = c;
    }
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        TrieNode *root = new TrieNode;
        for(auto &word: words) {
            buildTrie(word, root);
        }
        vector<string> ret;
        int i, j;
        for(i = 0; i < board.size(); ++i) {
            for(j = 0; j < board[0].size(); ++j) {
                dfs(i, j, board, ret, root);
            }
        }
        return ret;
    }
};
```
