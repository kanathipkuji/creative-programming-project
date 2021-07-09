# Factorial Trailing Zeroes
https://leetcode.com/problems/factorial-trailing-zeroes/

## Solution: Mathematical solution
### Language: Python 3

The number of trailing zeroes can be determined by counting the number of five multiples in from 1 to n. Also, we need to find the number of multiple of five squared and tripled and so on.
The summation of those numbers will be the answer.

```python3
class Solution:
    def trailingZeroes(self, n: int) -> int:
        fifth = 5
        ret = 0
        while fifth <= n:
            ret += n // fifth
            fifth *= 5              
        return ret
```

