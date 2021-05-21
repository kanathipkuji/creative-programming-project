# Decode Ways
https://leetcode.com/problems/decode-ways/

## Solution: Dynamic Programming
### Language: C++
### Time Complexity: O(n)

Define a state as follows.

* dp[i] is a number of ways to decode substring [0..i-1].

There are 2 types of state transitioning.

1. Decode a character of 1 digit. This occurs when the character at *i-1* is not zero, so we can derive the number of ways from dp[i - 1], i.e., dp[i] += dp[i - 1]
2. Decode a character of 2 digits. This is when a character at *i-2* and *i-1* forms a number that is in the range [10..26]. In this case, dp[i] += dp[i - 2]

The final answer is dp[n] derived by the state previously defined.

```c++
class Solution {
public:
    int numDecodings(string s) {
        int n = s.size();
        vector<int> dp(n + 1);
        if (s[0] == '0') return 0;
        dp[0] = 1;
        for (int i = 1; i <= n; ++i) {
            if (s[i - 1] != '0') {
                dp[i] = dp[i - 1];
            }
            if (i > 1 && (s[i - 2] == '1' || s[i - 2] == '2' && s[i - 1] <= '6')) {
                dp[i] += dp[i - 2];
            }
        }
        return dp[n];
    }
};```

