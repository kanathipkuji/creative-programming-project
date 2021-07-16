# Missing Number
https://leetcode.com/problems/missing-number/

## 1st Solution: Virtual Indexing
### Language: Python 3
### Time Complexity: O(n)

For each element in the list, we negate the value of index represented by that number. As a result, the index at which its corresponding number is not negated, is the answer.
But zeroes have to be treated differently as there are no differences between zero and its negation.

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

## 2nd Solution: Summation Difference
### Language: Python 3
### Time Complexity: O(n)

The difference between sum from 1..n and the sum of the list, will be the answer.

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

