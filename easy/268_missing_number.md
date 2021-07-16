# Missing Number
https://leetcode.com/problems/missing-number/

## Solution: Mathematical solution
### Language: Python 3

The number of trailing zeroes can be determined by counting the number of five multiples in from 1 to n. Also, we need to find the number of multiple of five squared and tripled and so on.
The summation of those numbers will be the answer.

```python3
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        allLess = True
        zeroIndex = -1
        for i, num in enumerate(nums):
            if abs(num) >= len(nums):
                allLess = False
                continue
            if num == 0:
                zeroIndex = i
            nums[abs(num)] *= -1
        for i, num in enumerate(nums):
            if num > 0:
                return i
        return (0 if zeroIndex == a-1 else zeroIndex) if not allLess else len(nums)
```

