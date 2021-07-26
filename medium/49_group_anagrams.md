# Group Anagrams
https://leetcode.com/problems/group-anagrams/

## Solution: Sorting Copied Strings
### Language: C++
### Time Complexity: O(nlogn)

The code below shows a straight-forward implementation: copy each string, sort it, and sort the whole array. Then, iteratively find unique sorted string. In order to map this with the old strings, we need to store it as an index.

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        int sz = strs.size();
        vector<vector<string>> ans{};
        if (!sz) {
            return ans;
        }
        vector<int> idx(strs.size());
        iota(begin(idx), end(idx), 0);
        vector<string> charSortedStrs(strs);
        for(auto &s: charSortedStrs) {
            sort(begin(s), end(s));
        }
        sort(begin(idx), end(idx), [&charSortedStrs](const auto &x, const auto &y) {
            return charSortedStrs[x] < charSortedStrs[y];
        });
        // for(auto& i: idx) {
        //     cout << "HERE: at " << i << ": " << charSortedStrs.at(i) << endl;
        // }

        vector<string> subAns;
        int id = 0;
        subAns.emplace_back(strs[idx[0]]);
        for (int i = 1; i < sz; ++i) {
            if (charSortedStrs[idx[i]] != charSortedStrs[idx[i - 1]]) {
                ans.emplace_back(subAns);
                subAns.clear();
                ++id;
            }
            subAns.emplace_back(strs[idx[i]]);
        }
        ans.emplace_back(subAns);
        return ans;
    }
};
```
