# Pascal's Triangle
https://leetcode.com/problems/pascals-triangle/

## Solution: Iterative Solution
### Language: Python 3

Every unit of the Pascal Triangle is a sum of its upper unit and the one prior to it.

```python3
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        ret = [[1]]
        for i in range(numRows - 1):
            ret.append([1])
            for j in range(1, i + 1):
                ret[-1].append(ret[-2][j - 1] + ret[-2][j])
            ret[-1].append(1)
        return ret
```

