# 3Sum Closest
https://leetcode.com/problems/3sum-closest/

## Solution: Two Pointers
### Language: Python3
### Time Complexity: O(n^2)

The idea is similar to "3Sum" where we loop through each number and use two-pointers technique for to find the other 2 integers.
To understand why we can move pointers this way, let consider the following scenario.

* sum := nums[i] + nums[l] + nums[r] is less than target

In this case, it is pointless to decrement r because it will result in *sum* being less. Thus, we increment l by 1.
Same idea hold for the opposite case.

```python3
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        diff = float('inf')
        n = len(nums)
        
        for i in range(n):
            l, r = i + 1, n - 1
            
            while l < r:
                sum = nums[i] + nums[l] + nums[r]
                if abs(diff) > abs(target - sum):
                    diff = target - sum
                if sum < target:
                    l += 1
                else:
                    r -= 1
            if diff == 0: break
        return target - diff
```

