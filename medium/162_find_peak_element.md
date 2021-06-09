# Find Peak Element
https://leetcode.com/problems/find-peak-element/

## Solution: Binary Search
### Language: Python3
### Time Complexity: O(log n) where n is the size of the array.

Binary search can return the index of one of the peak nodes, even though the array to be searched is not sorted.
The reason it works is because if nums[mid] < nums[mid + 1], one of peak elements has to exist somewhere between mid + 1 and r.
In the worst case, it will reach the boundary where mid = len(nums) - 1, but this will be a peak element according to the problem's statement.
The argument holds for both left and right side. So, with binary search, we can keep a subarray that has to contain a peak element.
Eventually, that subarray with size 1 is the answer to the problem.

```python3
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        n = len(nums)
        l, r = 0, n - 1
        
        while l < r:
            mid = (l + r) // 2
            if nums[mid] < nums[mid + 1]:
                l = mid + 1
            else:
                r = mid
            
        return l
```

