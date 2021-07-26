# Maximum Product Subarray
https://leetcode.com/problems/maximum-product-subarray/

## Solution: Dynamic Programming
### Language: Python 3
### Time Complexity: O(n)

There are 2 cases for each integer: its value is positive and negative. In the case where it is positive, maximum product can be deduced from the last maximum product times itself. But in the other case, maximum product should be calculated from the last minimum product. 

```python3
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        mn = [0] * n
        mx = [0] * n
        mn[0] = mx[0] = nums[0]
        for i in range(1, n):
            if nums[i] > 0:
                mn[i] = min(mn[i - 1] * nums[i], nums[i])
                mx[i] = max(mx[i - 1] * nums[i], nums[i])
            else:
                mx[i] = max(mn[i - 1] * nums[i], nums[i])
                mn[i] = min(mx[i - 1] * nums[i], nums[i])
        return max(mx)
```

