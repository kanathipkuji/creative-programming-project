# Increasing Triplet Subsequence
https://leetcode.com/problems/increasing-triplet-subsequence/

## Solution
### Language: Python3
### Time Complexity: O(n)

*   Let dp[i] be the length of LIS that ends at nums[i].
*   dp[i] equals the maximum of dp[j] + 1 (j < i) when nums[j] < nums[i]
*   in which case nums[i] can be appended to the increasing subsequence ending at j. 

```
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        first = nums[0]
        noSecond = True
        for num in nums:
            if num <= first:
                first = num
            elif noSecond or num <= second:
                second = num
                noSecond = False
            else:
                return True
        return False
```
