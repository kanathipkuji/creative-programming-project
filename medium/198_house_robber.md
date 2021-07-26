# House Robber
https://leetcode.com/problems/house-robber/

## Solution: Dynamic Programming
### Language: Python 3
### Time Complexity: O(n)

The following code uses 2 dynamic states. One stores the answer considering the previous house, while the other stores the answer not considering it.

```python3
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        lenn = len(nums)
        dp = [0] * (lenn + 1)
        dp1 = [0] * (lenn + 1)
        for i, num in enumerate(nums, 1):
            dp[i] = dp1[i - 1] + num
            dp1[i] = max(dp1[i - 1], dp[i - 1])
        return max(dp[lenn], dp1[lenn])
```

