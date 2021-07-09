# Best Time to Buy and Sell Stock II
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

## Solution: Dynamic Programming
### Language: C++
### Time Complexity: O(n)

Define dp[i] as maximum profit gained in i-th day.
There are 2 scenarios: selling and not selling stock on i-th day.
The profit gained can be calculated by taking dp[i-1] and prices[i-1] into account.

```c++
class Solution {
public:
    int dp[100005]{};
    int maxProfit(vector<int>& prices) {
        int num = prices.size();
        if(!num) return 0;
        int mx = -prices[0];
        for (int i = 2; i <= num; ++i) {
            dp[i] = max(mx + prices[i - 1], dp[i - 1]);
            mx = max(mx, dp[i - 1] - prices[i - 1]);
        }
        return dp[num]; 
    }
};
```

