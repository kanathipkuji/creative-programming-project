# Jump Game
https://leetcode.com/problems/jump-game/

## Solution: Backward Iteration
### Language: Python 3
### Time Complexity: O(nlogn)

Instead of forwardly solving the problem, this solution solve it from behind. First, assume that the last index is reacheable. In this case, we can try to find, from the last index, the index at which the value satisfies this assumption. Namely, if *i + nums[i] >= l*, this means i-th value contributes to l being reacheable. As a result, the last index is reacheable if and only if *l == 0*. In other words, the first node contributes to the last node being reacheable.

```python3
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        l = n - 1
        for i in range(n - 1, -1, -1):
            if i + nums[i] >= l:
                l = i
        return l == 0
```
