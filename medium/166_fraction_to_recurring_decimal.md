# Fraction to Recurring Decimal
https://leetcode.com/problems/fraction-to-recurring-decimal/

## Solution: Hashing Numerators
### Language: Python3

First, notice that there is no need to insert the period '.' when numerator can be divided by denominator, in which case we return the value as a string without performing further actions.

```python3
class Solution:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        if numerator == 0: return '0'
        if numerator % denominator == 0:
            return str(numerator // denominator)
        ret = ''
        if numerator // denominator < 0:
            ret += '-'
        numerator = abs(numerator)
        denominator = abs(denominator)
        
        ret += str(numerator // denominator)
        ret += '.'
        
        vis = defaultdict(int)
        numerator %= denominator
        
        while numerator > 0:
            if vis[numerator] == 0:
                vis[numerator] = len(ret)
            else:
                idx = vis[numerator]
                return ret[:idx] + '(' + ret[idx:] + ')'
            
            numerator *= 10
            ret += str(numerator // denominator)
            numerator %= denominator
            
        return ret
```

