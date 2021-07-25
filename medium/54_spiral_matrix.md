# Spiral Matrix
https://leetcode.com/problems/spiral-matrix/

## Solution: List Zipping
### Language: Python 3

The code below solves the problem by deleting the first row of the current list while tranpose and invert (flip) the list.
We call zip(\*matrix) to transpose the matrix as zip() maps each row of the list as a new element.

```python3
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ret = []
        while matrix:
            ret.extend(matrix[0])
            matrix.pop(0)
            matrix = [*zip(*matrix)][::-1]
        return ret
```

