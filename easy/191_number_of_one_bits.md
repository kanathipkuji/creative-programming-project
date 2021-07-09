# Number of 1 Bits
https://leetcode.com/problems/number-of-1-bits/

## Solution: Bitwise Operation
### Language: Python 3

When the number *n* *and* with its negative value, it will be a number containing the last 1 bit of *n*.

```python3
class Solution:
    def hammingWeight(self, n: int) -> int:
        ret = 0
        while n > 0:
            ret += 1
            n -= n & -n
        return ret
```

