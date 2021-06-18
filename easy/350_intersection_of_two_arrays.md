# Intersection of Two Arrays II
https://leetcode.com/problems/intersection-of-two-arrays-ii/

## Solution: Utilizing Python's built-in container
### Language: Python3

```python3
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list((Counter(nums1) & Counter(nums2)).elements())
```

