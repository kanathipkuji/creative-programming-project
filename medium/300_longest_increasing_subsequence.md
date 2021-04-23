# Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence/


## 1st Solution: Dynamic Programming
### Language: Python3
### Time Complexity: O(n^2)

*   Let dp[i] be the length of LIS that ends at nums[i].
*   dp[i] equals the maximum of dp[j] + 1 (j < i) when nums[j] < nums[i]
*   in which case nums[i] can be appended to the increasing subsequence ending at j. 

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


## 2nd Solution: Dynamic Programming
### Language: Python3
### Time Complexity: O(nlogn)

*   Create an array which is always sorted in ascending order with the following properties.
*   Element at index *i* stores a tail (last element) of IS with length *i* + 1.
*   Thus, the length of LIS is equal to the length of IS at index *n* - 1 of the previously defined array.

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        v = []
        for num in nums:
            idx = bisect_left(v, num)
            if idx == len(v):
                v.append(num)
            else:
                v[idx] = num
        return len(v)
```

