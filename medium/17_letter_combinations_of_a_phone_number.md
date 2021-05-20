# Letter Combinations of a Phone Number
https://leetcode.com/problems/letter-combinations-of-a-phone-number/

## Solution: Complete Search
### Language: C++

The code below shows a DFS implementation with the help of *letters* to facilitate the process of picking characters.

```c++
class Solution {
    const vector<string> letters{"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    void dfs(const string& digits, vector<string>& res, string& cur, int idx=0) {
        if (idx == digits.length()) {
            res.push_back(cur);
            return;
        }
        int digit = digits[idx] - '0';
        for (auto c: letters[digit - 2]) {
            cur += c;
            dfs(digits, res, cur, idx + 1);
            cur.pop_back();
        }
    }
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        string cur = "";
        vector<string> res;
        dfs(digits, res, cur);
        return res;
    }
};
```

