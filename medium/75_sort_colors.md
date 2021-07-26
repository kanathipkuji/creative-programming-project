# Sort Colors
https://leetcode.com/problems/sort-colors/

## Solution: 3-pointers
### Language: C++
### Time Complexity: O(n)

The code below maintains 3 pointers such that the each one point to 0, 1, 2 separately. More specifically, *l* points to the first value after 0, *i* points to the first unclassified elements, and *r* poitns to the last value before 2.

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int l = 0, r = nums.size() - 1, i = 0;
        while(i <= r) {
            if(nums[i] == 0) {
                swap(nums[l], nums[i]);
                ++i, ++l;
            } else if(nums[i] == 1) {
                ++i;
            } else {
                swap(nums[r], nums[i]);
                --r;
            }
        }
    }
};
```
