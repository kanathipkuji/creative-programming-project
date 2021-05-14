# Container With Most Water
https://leetcode.com/problems/container-with-most-water/

## Solution: Two Pointers
### Language: Python3
### Time Complexity: O(n)

* Two pointers pointing at both ends of the list.
* The pointer of pointing to a value of smaller height should be moved.
* The reason is when the height is higher on one side, moving it would not affect the height of the tank, but would result in the decrease in length.
* Thus, this greedy algorithm works.

```python3
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        ret = 0
        while l < r:
            ret = max(ret, (r - l) * min(height[l], height[r]))
            
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
            
        return ret
```

