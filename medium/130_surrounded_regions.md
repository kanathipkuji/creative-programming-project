# Surrounded Regions
https://leetcode.com/problems/surrounded-regions/

## Solution: Flood Fill
### Language: C++

The code below performs depth first search from every edge of the grid if its value is 'O', and flag cells that has been traveled as "true". Finally, unflagged 'O' cells must be surrounded by 'X',

```c++
class Solution {
    constexpr static int gx[4] = {-1, 1, 0, 0};
    constexpr static int gy[4] = {0, 0, -1, 1};
    vector<vector<bool>> dp;
    void dfs(vector<vector<char>>& board, int x, int y) {
        if(board[x][y] != 'O') return;
        int xx, yy;
        dp[x][y] = true;
        for(int i = 0; i < 4; ++i) {
            xx = x + gx[i];
            yy = y + gy[i];
            if(xx < 0 || xx >= board.size() || yy < 0 || yy >= board[0].size()
                || board[xx][yy] == 'X' || dp[xx][yy])
                continue;
            dfs(board, xx, yy);
        }
    }
public:
    void solve(vector<vector<char>>& board) {
        if(board.empty())
            return;
        int n = board.size(), m = board[0].size(), i, j;
        dp.assign(n, vector<bool>(m));
        for(i = 0; i < n; ++i) {
            dfs(board, i, 0);
            dfs(board, i, m - 1);
        }
        for(i = 0; i < m; ++i) {
            dfs(board, 0, i);
            dfs(board, n - 1, i);
        }
        for(i = 0; i < n; ++i) {
            for(j = 0; j < m; ++j) {
                if(dp[i][j])
                     continue;
                board[i][j] = 'X';
            }
        }
    }
};
```

