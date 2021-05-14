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
