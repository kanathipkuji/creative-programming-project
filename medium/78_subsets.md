# Subsets
https://leetcode.com/problems/subsets/

## Solution: Iterative Solution using Bitmask
### Language: C++
### Time Complexity: O(n * 2 ^ n)

The solution is to find all permutations of all lengths of the given array. One way to solve this, is to store a permutation in one integer as a bitmask.

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int n = 1 << nums.size(), size = nums.size(), j;
        vector<vector<int>> ret;
        for(int i = 0; i < n; ++i) {
            vector<int> v;
            for(j = 0; (1<<j) < n; ++j) {
                if(i & (1<<j)) {
                    v.push_back(nums[j]);
                }
            }
            ret.push_back(v);
        }
        return ret;
    }
};
```
