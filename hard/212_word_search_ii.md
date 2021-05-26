# Word Search
https://leetcode.com/problems/word-search-ii/

## 1st Solution: Trie
### Language: C++
### Time Complexity: O(mn * 4^k) where k is maximum length of a word

We create a Trie which is a tree that contains a letter on each edges (or can be implemented to contains on each vertices). The characters of the edges through which traversal from the root node to the current node passes, represents a word. If there is a word ending at the current node, store the word to the node. Otherwise, the node does not store the word. For example, if the word list contains "A", "DO", "DID", "BO", "BA", "DOG"; the trie would be constructed as shown. 

![Trie](https://user-images.githubusercontent.com/60181774/119641191-5ce56580-be54-11eb-8a1e-f520ae935640.png)

Now, to search for words in the table that are also exist in Trie, it is easier to implement by DFS (Depth First Search). However, in order to avoid re-visiting the node, we change the value of the current cell to be '-', and after processing all its children, change it back to the previous value. It the value of the current cell matches the value of the node in the trie containg a word, then that word is one of the answer.

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
            dfs(x, y + 1, board, ret, root);
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
