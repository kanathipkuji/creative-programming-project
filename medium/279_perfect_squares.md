# Perfect Squares
https://leetcode.com/problems/perfect-squares/

## Solution: 0-1 Knapsack
### Language: C++
### Time Complexity: O(n)

We generate a number of square numbers. After that, utilize knapsack dynamic programming to find minimum steps to reach the current weight. In this case, the weight is the number corresponding to the index itself.

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1), v(sqrt(n));
        int a = 1;
        generate(v.begin(), v.end(), [&a]() {
            return a*(a++);
        });
        int i;
        for(auto &x: v) {
            // cout << x << endl;
            for(i = x; i <= n; ++i) {
                if(dp[i] == 0 || dp[i] > dp[i - x] + 1) {
                    dp[i] = dp[i - x] + 1;
                }
            }
        }
        return dp[n];
    }
};
```
