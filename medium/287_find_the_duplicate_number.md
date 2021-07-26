# Find the Duplicate Number
https://leetcode.com/problems/find-the-duplicate-number/

## Solution: Sorting
### Language: C++
### Time Complexity: O(nlogn)

Sorting can be used to find a duplicate number as every pair of elements that is adjacent to each other after sorted should be compared at least once.

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int ans;
        sort(nums.begin(), nums.end(), [&](int x, int y) {
           if(x == y)
               ans = x;
            return x < y;
        });
        return ans;
    }
};
```
