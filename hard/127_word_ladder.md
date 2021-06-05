# Word Ladder
https://leetcode.com/problems/word-ladder/

## Solution: Breadth First Search
### Language: C++
### Time Complexity: O(n*n*len) where n is the size of the word list and len is the length of each word.

We construct a path from a node corresponding to *beginWord*, and iterate through nodes satisfying *differByOne* function which checks if two strings differ by one letter. The final node is *endWord*. Breadth First Traversal is a key to reach the final node with minimum steps possible.
Finally, the minimum step is the answer.

```c++
class Solution {
    bool differByOne(const string& a, const string& b) {
        int diff = 0;
        for (int i = 0; i < a.size(); ++i) {
            if (a[i] != b[i]) {
                ++diff;
                if (diff > 1) return false;
            }
        }
        return diff == 1;
    }
    
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        queue<int> q;
        vector<int> dist(wordList.size() + 1);
        q.push(0);
        dist[0] = 1;
        int cur;
        string u;
        while (!q.empty()) {
            cur = q.front();
            q.pop();
            if (!cur) {
                u = beginWord;
            } else {
                if (wordList[cur - 1] == endWord)
                    return dist[cur];
                u = wordList[cur - 1];
            }
            for (int i = 0; i < wordList.size(); ++i) {
                if (differByOne(u, wordList[i])) {
                    if (!dist[i + 1]) {
                        dist[i + 1] = dist[cur] + 1;
                        q.emplace(i + 1);
                    }
                }
            }
        }
        return 0;
    }
};
```

## 2nd Solution: Optimized Breadth First Search
### Language: C++
### Time Complexity: O(n*len) where n is the size of the word list and len is the length of each word.

The first solution is inefficiency due to its algorithm to find next node. In this solution, instead of looping through all words in the list, we try to find if the word modified from the current one, exists in the word list.
If so, we add it to the queue. This way it loops only 26 times per each character.

```c++
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        queue<string> q;
        unordered_set<string> uset(wordList.begin(), wordList.end());
        q.push(beginWord);
        int ret = 0, sz;
        char c;
        while (!q.empty()) {
            ++ret;
            sz = q.size();
            while (sz--) {
                string u = q.front();
                q.pop();

                if (u == endWord) return ret;
                for (auto& curChar: u) {
                    c = curChar;
                    for (int j = 0; j < 26; ++j) {
                        if (curChar - 'a' == j) continue;
                        curChar = j + 'a';
                        auto it = uset.find(u);
                        if (it != uset.end()) {
                            q.push(u);
                            uset.erase(it);
                        }
                    }
                    curChar = c;
                }
            }
        }
        return 0;
    }
};
```


