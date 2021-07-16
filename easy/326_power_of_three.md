# Power of Three
https://leetcode.com/problems/power-of-three/

## Solution: Stable Partition
### Language: Python 3

The maximum number of power of three that can be contained in an integer-type is 3 ** 19. Thus, any integers dividing this number is a power of three.

```python3
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        return n > 0 and (3 ** 19) % n == 0
```

