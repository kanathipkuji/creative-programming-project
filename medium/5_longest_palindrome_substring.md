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



## 2nd Solution: Quick Select and virtual indexing
### Language: Python3
### Time Complexity: O(n) on average

With the objective to partition the array into two groups using median as a pivot, there is no need to sort the array. Instead, we can utilize quick selection algorithm to pick a median withing O(n) time complexity on average.

Then we need to devise a way to place elements in each group into the result array.
Consider the following methods.

1. Elements smaller than the median -> put into the last even index
2. Elements larger than the median -> put into the first odd index
3. The rest elements are to put into the remaining indices.

We can achieve this by using virtual indexing as follows.

* Old indices map to new indices by mapping the current index to the odd new index first, otherwise it maps to the first even index, and so on. 

Now, we create 3 variables: i, l, r; to keep track of current element, leftmost available odd index, rightmost available even index, respectively.

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

