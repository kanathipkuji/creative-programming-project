# Wiggle Sort II
https://leetcode.com/problems/wiggle-sort-ii/

## Solution: 
### Language: Python3
### Time Complexity: O(nlogn)

*   By partitioning the array with a median as a pivot, one will get a subarray *l* with all elements less than or equal to those of another subarray *r*.
*   And by placing elements from *l* into odd indices, *r* into even indices, the array will be wiggly sorted.

```
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = (len(nums) + 1) // 2
        nums.sort()
        l = nums[:n][::-1]
        r = nums[n:][::-1]
        for i in range(n):
            nums[2 * i] = l[i]
            if 2 * i + 1 < len(nums):
                nums[2 * i + 1] = r[i]
            
```

