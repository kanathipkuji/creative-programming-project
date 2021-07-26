# Excel Sheet Column Title
https://leetcode.com/problems/excel-sheet-column-title/

## Solution: Base Convertion
### Language: Python 3

The problem can be reduced to base conversion problem where the base is 26. However, there is no zero in system so for every digit the number should be reduced by 1.

```python3
class Solution:
    def convertToTitle(self, columnNumber: int) -> str:
        ret = ''
        x = columnNumber
        while x > 0:
            ret += chr((x + 25) % 26 + ord('A'))
            x = (x - 1) // 26
            
        return ret[::-1]
```
