# Two Sum
https://leetcode.com/problems/find-the-duplicate-number/

## Solution: Two Pointers
### Language: C++
### Time Complexity: O(n)

First, set one pointer to the first, another to the last element of the sorted list. Then is the sum of two elements being pointed is greater than target value, then we must decrease the sum by decrementing the right pointer by 1, and vice versa. 

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        vector<int> indices(n);
        iota(indices.begin(), indices.end(), 0);
        sort(indices.begin(), indices.end(), [&](int x, int y) {
            return nums[x] < nums[y];
        });
        int l = 0;
        int r = n - 1;
        while (l < r) {
            int sum = nums[indices[l]] + nums[indices[r]];
            if (sum < target)
                ++l;
            else if (sum > target)
                --r;
            else {
                return {indices[l], indices[r]};
                break;
            }
        }
        return {};
    }
};
```
