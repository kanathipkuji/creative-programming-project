# Number of Ways to Wear Different Hats to Each Other
https://leetcode.com/problems/number-of-ways-to-wear-different-hats-to-each-other/

## Solution: Dynamic Programming with Bitmask
### Language: C++
### Time Complexity: O(nk2^n) where n is the number of people, and k is the number of different hats.

We store a subset of people as a key in a state.
Specifically, a state dp[S] store the number of different ways for people in subset S to wear different hats.
The answer of the problem is dp[(1 << n) - 1] which is the number of ways for all people to wear different hats.

```c++
class Solution {
public:
    int numberWays(vector<vector<int>>& hats) {
        int n = hats.size();
        int mod = 1e9 + 7;
        vector<vector<int>> hashMap(41);
        
        for (int i = 0; i < n; ++i) {
            for (int hat: hats[i]) {
                hashMap[hat].push_back(i);
            }
        }
        vector<int> dp(1 << n);
        dp[0] = 1;
        for (int hat = 0; hat <= 40; ++hat) {
            if (hashMap[hat].empty()) continue;
            for (int mask = (1 << n) - 1; mask >= 0; --mask) {
                for (int person: hashMap[hat]) {
                    if (!(mask & (1 << person))) {
                        dp[mask | (1 << person)] += dp[mask];
                        dp[mask | (1 << person)] %= mod;
                    }
                }
            }
        }
        return dp[(1 << n) - 1];
    }
};
```
