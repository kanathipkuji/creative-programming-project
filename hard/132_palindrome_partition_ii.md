# Palindrome Partitioning II
https://leetcode.com/problems/palindrome-partitioning-ii/

## Solution: Dynamic Programming
### Language: C++
### Time Complexity: O(n^2)

The code below is an implementation using dynamic programming.
We define the state dp[i] to be the number of minimum palindromic cut to substring [0..i - 1]. dp[0] is defined as -1.
The state transition is set as follows.

dp[i] = min(dp[i], dp[k] + 1) for every *k* that makes substring [k + 1..i - 1] a palindrome.

```c++
class Solution {
public:
    int minCut(string s) {
        int n = s.size();
        vector<int> dp(n + 1, 0);
        for (int i = 0; i <= n; ++i) {
            dp[i] = i - 1;
        }
        for (int i = 0; i < n; ++i) {
            dp[i + 1] = min(dp[i + 1], dp[i] + 1);
            for (int j = 1; i - j >= 0 && i + j < n && s[i + j] == s[i - j]; ++j) {
                dp[i + j + 1] = min(dp[i + j + 1], dp[i - j] + 1); 
            }    
            for (int j = 1; i - j + 1 >= 0 && i + j < n && s[i + j] == s[i - j + 1]; ++j) {
                dp[i + j + 1] = min(dp[i + j + 1], dp[i - j + 1] + 1); 
            }  
        }
        return dp[n];
    }
};
```
