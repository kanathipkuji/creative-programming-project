# Longest Palindrome Substring
https://leetcode.com/problems/longest-palindromic-substring/

## 1st Solution: Dynamic Programming
### Language: C++
### Time Complexity: O(n^2)
### Space Complexity: O(n^2)

Define *dp[l][r]* as follows.
* *True*, if the substring [l..r] is a palindrome
* *False*, Otherwise

The base case is dp[l][l] = true and dp[l][l + 1] = s[l] == s[l + 1].
Then, recursively assign dp[l][r] = (dp[l + 1][r - 1] and s[l] == s[r]) to transition the state.

The answer will be the substring [l..r] in which l and r are most distant and still makes dp[l][r] true.

```c++
class Solution {
    vector<vector<int>> dp;
    bool isPalindrome(const string& s, int l, int r) {
        if (dp[l][r] != -1) return dp[l][r];
        if (l == r) return dp[l][r] = true;
        if (l + 1 == r) return dp[l][r] = s[l] == s[r];
        return dp[l][r] = isPalindrome(s, l + 1, r - 1) && s[l] == s[r];
    }
public:
    string longestPalindrome(string s) {
        int n = s.length();
        int maxLen = 0;
        string ret = "";
        dp.assign(n, vector<int>(n, -1));
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j <= i; ++j) {
                if (isPalindrome(s, j, i)) {
                    if (maxLen < i - j + 1) {                        
                        maxLen = i - j + 1;
                        ret = s.substr(j, i - j + 1);
                    }
                }

            }
        }
        return ret;
    }
};
```



## 2nd Solution: Expand Around Center
### Language: C++
### Time Complexity: O(n^2)
### Space Complexity: O(1)

For each middle index of a palindrome, iterate in both left and right direction and stop if the characters in the left and right index do not match. There can only be *O(n)* indices, and the process takes *O(n)* for each middle index. Thus, the overall time complexity is *O(n^2)*. Auxiliary space is reduced from *O(n^2)* in dynamic programming approach to *O(1)*.

```c++
class Solution {
    int expandAroundCenter(const string& s, int l, int r) {
        int n = s.length();
        while (l >= 0 && r < n && s[l] == s[r]) {
            --l, ++r;
        }
        return r - l - 1;
    }
public:
    string longestPalindrome(string s) {
        int n = s.length();
        int maxLen = 0;
        string ret = "";
        for (int i = 0; i < n; ++i) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int len = max(len1, len2);
            if (maxLen < len) {
                maxLen = len;
                ret = s.substr(i - (len - 1) / 2, len);
            }
        }
        return ret;
    }
};
```

