# Sqrt(x)
https://leetcode.com/problems/sqrtx/

## Solution: Binary search
### Language: C++
### Time Complexity: O(log x)

We binary search the number that can square and has value more than or equal to x.

```python3
class Solution:
    def mySqrt(self, x: int) -> int:
        l, r = 0, x
        while l <= r:
            mid = l + (r - l) // 2
            if mid * mid <= x < (mid + 1) * (mid + 1):
                return mid
            if mid * mid > x:
                r = mid - 1
            else:
                l = mid + 1
        
```

