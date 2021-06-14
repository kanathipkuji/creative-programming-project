# Valid Sudoku
https://leetcode.com/problems/valid-sudoku/

## Solution: Hashing
### Language: C++

We store a number in 3 hash sets each of which contain 9 blocks. Those hash sets are for rows, columns, and blocks.
The calculation of the number of block *k* is given by k = 3 * (row / 3) + (col / 3).

```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        bool vis[3][9][9] = {};
        int k, cur;
        char c;
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                k = 3 * (i / 3) + (j / 3);
                c = board[i][j];
                if (c == '.') continue;
                cur = c - '1';                
                if (vis[0][i][cur] || vis[1][j][cur] || vis[2][k][cur])
                    return false;
                vis[0][i][cur] = vis[1][j][cur] = vis[2][k][cur] = true;
            }
        }
        return true;
    }
};
```

