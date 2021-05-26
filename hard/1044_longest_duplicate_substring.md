# Longest Duplicate Substring
https://leetcode.com/problems/longest-duplicate-substring/

## Solution: Binary Search with Rabin-Karp algorithm
### Language: C++
### Time Complexity: O(nlogn)

Rabin-Karp algorithm is an algorithm that stores substrings of a certain length in a hash table. With the algorithm we can binary search on length to find the longest length 
which produces a duplicate substring.


```c++
class Solution {
    constexpr static long long MUL = 26;
    constexpr static long long MOD = 19260817;
    
    bool check(string& S, int len, int& idx) {
        if(len == 0)
            return false;
        int i;
        long long p = 0, off = 1;
        unordered_map<long long, vector<int>> Map;
        for(i = 0; i < len; ++i) {
            p = p * MUL % MOD + (S[i] - 'a');
            p %= MOD;
            if(i < len - 1) {
                off = (off * MUL) % MOD;
            }
        }
        Map[p] = vector<int>(1, 0);
        
        for(i = len; i < S.size(); ++i) {
            p = ((p - (S[i - len] - 'a') * off) % MOD + MOD) % MOD;
            p = p * MUL + (S[i] - 'a');
            p %= MOD;
            if(Map.find(p) == Map.end()) {
                Map[p] = vector<int>(1, i - len + 1);
            } else {
                for(auto& x: Map[p]) {
                    if(strcmp((S.substr(x, len)).data(), S.substr(i - len + 1, len).data()) == 0) {
                        idx = x;
                        return true;
                    }
                }
                Map[p].push_back(i - len + 1);
            }
        }
        return false;
    }

public:
    string longestDupSubstring(string S) {
        int l = 0, r = S.size(), mid, idx;
        string ret = "", tmp;
        while(l <= r) {
            mid = l + (r - l) / 2;
            if(check(S, mid, idx)) {
                tmp = S.substr(idx, mid);
                if(ret.size() < tmp.size())
                    ret = tmp;
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        return ret;
    }
};
```
