# Trapping Rain Water
https://leetcode.com/problems/trapping-rain-water/

## Solution: Two Pointers
### Language: C++
### Time Complexity: O(n)
### Space Complexity: O(1)

At any given height, the height of water after the rain is necessarily equal to the minimum of maximum from the left and from the right.
So, we keep track of the maximum height from the left as well as from the right. 

```python3
class Solution:
    def trap(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        ret = 0
        maxL, maxR = 0, 0
        while l < r:
            if height[l] < height[r]:
                if height[l] >= maxL:
                    maxL = height[l]
                else:
                    ret += maxL - height[l]
                l += 1
            else:
                if height[r] >= maxR:
                    maxR = height[r]
                else:
                    ret += maxR - height[r]
                r -= 1
        return ret
    
```
