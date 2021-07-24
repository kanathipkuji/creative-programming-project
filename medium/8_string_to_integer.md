# String to Integer (atoi)
https://leetcode.com/problems/string-to-integer-atoi/

## Solution: Striping and Extracting Digits
### Language: Python 3

The solution tries to convert the given string into a string containing only digits, by striping leading space and check if the left string does not start with non-digit characters.

```python3
class Solution:
    def myAtoi(self, s: str) -> int:
        INT_MAX = (1 << 31) - 1
        INT_MIN = -INT_MAX - 1
        
        s = s.strip()
        if not s: return 0
        i = 0
        sign = 1
        digits = ""
        if s[i] == '-':
            i += 1
            digits += '-'
        elif s[i] == '+':
            i += 1
        if i >= len(s) or not s[i].isdigit():
            return 0
        while i < len(s) and s[i].isdigit():
            digits += s[i]
            i += 1
        
        return max(INT_MIN, min(INT_MAX, int(digits)))

```

