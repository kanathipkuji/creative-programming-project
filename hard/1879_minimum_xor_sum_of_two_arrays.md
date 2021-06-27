# Minimum XOR Sum of Two Arrays
https://leetcode.com/problems/minimum-xor-sum-of-two-arrays/

## Solution: Dynamic Programming with Bitmask
### Language: C++
### Time Complexity: O(n2^n)

We define a state dp[mask][lv] to be the minimum XOR sum of the subarray nums1[0..(lv-1)] and the subset represented by 0-bits in *mask*.
However, the second dimension can be omitted to save memory.
The state transition is defined as follows.

* dp[mask][lv] = min(dp[mask | (1 << i)][lv + 1] + (nums1[lv] ^ nums2[i]))

As such, the root state is dp[mask][n] = 0.


```c++
class Solution {
    vector<int> dp;
    
public:
    int minimumXORSum(vector<int>& nums1, vector<int>& nums2) {
        dp.assign(1 << 14, INT_MAX);
        return minimumXORSum(nums1, nums2, 0, 0);
    }
    
    int minimumXORSum(vector<int>& nums1, vector<int>& nums2, int lv, int mask) {
        if (dp[mask] != INT_MAX) return dp[mask];
        if (lv == nums1.size()) return 0;
        int n = nums2.size();
        for (int i = 0; i < n; ++i) {
            if (!(mask & (1 << i))) {
                dp[mask] = min(dp[mask], minimumXORSum(nums1, nums2, lv + 1, mask | (1 << i)) + (nums1[lv] ^ nums2[i]));
            }
        }
        return dp[mask];
    }
};
```
