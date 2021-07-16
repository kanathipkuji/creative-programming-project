# Merge Sorted Array
https://leetcode.com/problems/merge-sorted-array/

## Solution: Reverse Sorting
### Language: Python 3
### Time Complexity: O(n + m)
### Space Complexity: O(1)

The solution is to recursively choose the minimum elements from 2 of the rightmost elements of 2 arrays.  

```python3
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        l, r = m - 1, n - 1
        count = 1
        while l >= 0 and r >= 0:
            if nums1[l] <= nums2[r]:
                nums1[m + n - count] = nums2[r]
                r -= 1
            else:
                nums1[m + n - count] = nums1[l]
                l -= 1
            count += 1
        while r >= 0:
            nums1[m + n - count] = nums2[r]
            r -= 1
            count += 1
```

