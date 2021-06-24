# Longest Common Prefix
https://leetcode.com/problems/longest-common-prefix/

## Solution: Double Loop
### Language: C++
### Time Complexity: O(nk) where k is the length of the answer, and n is a number of strings.

First, find the minimum length of all strings and set it as the upper bound for the iterator *i*.
Next, for each *i*, loop through all strings and see if all characters at index *i* still match.
If not, return the substring of range [0..i] (which is the same for all strings).

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string prev = "";
        int minLen = INT_MAX;
        for (auto& str: strs) {
            minLen = min(minLen, (int)str.size());
        }
        for (int i = 0; i < minLen; ++i) {
            for (auto& str: strs) {
                if (i >= str.size())
                    return prev;
                if (prev.size() <= i) {
                    prev += str[i];
                }
                if (prev[i] != str[i]) {
                    return prev.substr(0, i);
                }
            }
        }
        return prev;
    }
};
```

