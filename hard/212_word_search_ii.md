


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
