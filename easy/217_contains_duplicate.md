# Contains Duplicate
https://leetcode.com/problems/contains-duplicate/

## Solution: One-line Solution
### Language: Python 3

The array contains duplicate numbers if the size of its set is not equal to the size of the array itself.

```python3
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return len(nums) != len(set(nums))
            
```

