# Set Matrix Zeroes
https://leetcode.com/problems/set-matrix-zeroes/

## Solution: Hashing row and column indices that contain zeroes
### Language: Python3
### Time Complexity: O(mn)
### Space Complexity: O(m + n)

During matrix iteration, if zero is encountered, mark its row and column. On the second iteration, check if the row or column has been marked or not. If so, change the value of the cell to zero.

```python3
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        m = len(matrix[0])
        visRow = [0] * n
        visCol = [0] * m
        for i in range(n):
            for j in range(m):
                if matrix[i][j] == 0:
                    visRow[i] = 1
                    visCol[j] = 1
        
        for i in range(n):
            for j in range(m):
                if visRow[i] == 1 or visCol[j] == 1:
                    matrix[i][j] = 0
```

