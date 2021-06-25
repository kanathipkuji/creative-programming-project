# Unique Path II
https://leetcode.com/problems/unique-paths-ii/

### Solution: Dynamic Programming
## Language: C++
## Time Complexity: O(nm)

The dynamic programming is defined as dp[i][j] = the number of path reaching index [i][j].
The transition is defined as dp[i][j] = dp[i-1][j] + dp[i][j-1].

```
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if (obstacleGrid[0][0]) return 0;
        vector<vector<int>> dp;
        int n = obstacleGrid.size();
        int m = obstacleGrid[0].size();                                                                                                            
        dp.assign(n + 1, vector<int>(m + 1));
        dp[1][1] = 1;
        for (int i = 1; i <= n; ++i) {
            for (int j = 1; j <= m; ++j) {
                if (i == 1 && j == 1) continue;
                if (!obstacleGrid[i - 1][j - 1])
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[n][m];
    }
};
```
