# Find First and Last Position of Element in Sorted Array
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

## Solution: Lower Bound and Upper Bound
### Language: C++

The range of the same value can be determined by the range of upper-bound value and lower-bound value.

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int r = upper_bound(nums.begin(), nums.end(), target) - nums.begin();
        int l = lower_bound(nums.begin(), nums.end(), target) - nums.begin();
        if (l == r) {
            return {-1, -1};
        }
        return {l, r - 1};
    }
};
```

