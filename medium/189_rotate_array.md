# Rotate Array
https://leetcode.com/problems/rotate-array/

## Solution: Python List Slicing
### Language: Python 3

After the rotation, the first portion of the list corresponds to *nums[:-k]* whereas the second portion corresponds to *nums[-k:]*.

```python3
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        k %= len(nums)
        nums[:] = nums[-k:] + nums[:-k]
```

