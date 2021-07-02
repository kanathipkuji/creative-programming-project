# Roman to Integer
https://leetcode.com/problems/roman-to-integer/

## Solution: Storing values on an array
### Language: Python 3
### Time Complexity: O(n)

We process the value character by character while checking if it should be subtracted or not by looking into the previous character.
If its value is less than the current one, then it should be subtracted.

```python3
class Solution:
    def romanToInt(self, s: str) -> int:
        romanToInt = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        ret = 0
        n = len(s)
        for i in range(n):
            if i > 0 and romanToInt[s[i]] > romanToInt[s[i - 1]]:
                ret += romanToInt[s[i]] - 2 * romanToInt[s[i - 1]]
            else:
                ret += romanToInt[s[i]]
        return ret
```

