# Jump Game II
https://leetcode.com/problems/jump-game-ii/

## Solution: Interval Covering
### Language: Python3
### Time Complexity: O(n)

*   View the input as a set of intervals each of which is [i, i + nums[i]].
*   Apply greedy algorithms to compute minimum intervals to cover range [0, n - 1] as follows.
1. Select the first interval (given intervals are sorted)
2. For all intervals intercepting the selected one, find the interval with rightmost end, and select that interval.
3. Repeat 2 until all [0, n - 1] is covered or there are no intervals left.

```python3
class Solution:
    def jump(self, nums: List[int]) -> int:
        r = nextR = i = 0
        n = len(nums)
        ret = 0
        while i < n:
            while i < n and i <= r:
                nextR = max(nextR, nums[i] + i)
                i += 1
            if nextR >= r: break
            r = nextR
            ret += 1
            if r >= n - 1: break
        return ret
```
