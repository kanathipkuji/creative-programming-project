# Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence/


## 1st Solution: Dynamic Programming
### Language: Python3
### Time Complexity: O(n^2)

*   

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [1] * n
        ans = 1
        for i in range(n):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
                    ans = max(ans, dp[i])       
        return ans
```
