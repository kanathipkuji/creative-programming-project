# Isomorphic Strings
https://leetcode.com/problems/isomorphic-strings/

## Solution: Character Mapping
### Language: C++

We create a map table to map characters from *s* to *t*, and from *t* to *s*. When the mapping from *s* to *t* contradicts with the previously mapped value, then return false.

```c++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        vector<int> hashMap1(256, -1), hashMap2(256, -1);
        int n = s.size();
        for (int i = 0; i < n; ++i) {
            if (hashMap1[s[i]] != hashMap2[t[i]]) return false;
            hashMap1[s[i]] = i;
            hashMap2[t[i]] = i;
        }
        return true;
    }
};
```
