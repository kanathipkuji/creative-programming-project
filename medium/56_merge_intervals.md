# Merge Intervals
https://leetcode.com/problems/merge-intervals/

## Solution: Sorting and Interval Union
### Language: C++

This solution is straighforward: sort the interval in ascending order, then iteratively maintain a range that intervals are intercepting. 

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.empty()) return {};
        sort(intervals.begin(), intervals.end());
        int n = intervals.size();
        int l = intervals[0][0], r = intervals[0][1];
        vector<vector<int>> ret;
        int ll, rr;
        for (int i = 1; i < n; ++i) {
            ll = intervals[i][0];
            rr = intervals[i][1];
            
            if (r >= ll) {
                r = max(r, rr);    
            } else {
                ret.push_back(vector<int>{l, r});
                l = ll, r = rr;
            }
        }
        ret.push_back(vector<int>{l, r});
        return ret;
    }
};
```

