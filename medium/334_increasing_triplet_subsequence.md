# Increasing Triplet Subsequence
https://leetcode.com/problems/increasing-triplet-subsequence/

## Solution
### Language: Python3
### Time Complexity: O(n)

*   Store values that could belong to the first and second element of a increasing (duplet) subsequence in *first* and *second* respectively.
*   Note that, *first* and *second* can be values of elements from different subsequence. 
*   If there is an element greater than *second* then an increasing triplet subsequence exists.

```python3
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        first = nums[0]
        noSecond = True
        for num in nums:
            if num <= first:
                first = num
            elif noSecond or num <= second:
                second = num
                noSecond = False
            else:
                return True
        return False
```
