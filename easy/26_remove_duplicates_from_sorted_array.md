# Remove Duplicates from Sorted Array
https://leetcode.com/problems/remove-duplicates-from-sorted-array/

## Solution: Maintain a pointer
### Language: Python 3
### Time Complexity: O(n)

We maintain a pointer such that it always points to the index that the next unique number will be placed in.
Also, the number of unique numbers can be derived from the index itself.

```python3
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums: return 0
        n = len(nums)
        idx = 0
        prev = nums[0]
        for i in range(1, n):
            if nums[i] > prev:
                prev = nums[i]
                nums[i], nums[idx + 1] = nums[idx + 1], nums[i]
                idx += 1
        return idx + 1
```

