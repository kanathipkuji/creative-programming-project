# Contains Duplicate II
https://leetcode.com/problems/contains-duplicate-ii/

## Solution: Using Python Dictionary
### Language: Python 3

The dictionary here is used to store the most recent index of the value.
We return true if the value is already in the dictionary and the index differs by no more than k.

```python3
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        hashMap = {}
        for i, num in enumerate(nums):
            if num in hashMap and i - hashMap[num] <= k:
                return True
            hashMap[num] = i
        return False
```
