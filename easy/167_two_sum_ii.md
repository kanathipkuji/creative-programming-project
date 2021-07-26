# Two Sum II - Input array is sorted
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Solution: Two Pointers
### Language: Python 3
### Time Complexity: O(n)

This solution is the same as normal two sum problem.
We maintain two pointers such that if sum of pointed values is less than the target, the left one is incremented, and vice versa. 

```python3
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1
        while l < r:
            if numbers[l] + numbers[r] > target:
                r -= 1
            elif numbers[l] + numbers[r] < target:
                l += 1
            else:
                return [l + 1, r + 1]
```
