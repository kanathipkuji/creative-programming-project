# Set Matrix Zeroes
https://leetcode.com/problems/set-matrix-zeroes/

## 1st Solution: Hashing row and column indices that contain zeroes
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

## 2nd Solution: Marking on the first row or column
### Language: Python3
### Time Complexity: O(mn)
### Space Complexity: O(1)

If the cell is zero, marked its row and column as zero, so that in another iteration we can change those rows or columns to zeroes.
However, we have to handle the case where the first row or column contain zeroes as it would create an over-counting situation where matrix[0][0] is marked, and result in all columns of the first row and all rows of the first column getting changed to zeroes. To avoid this, we handle it separately by using two boolean variables to keep if it is the rows or columns (or both) that should be changed.

```python3
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        m = len(matrix[0])
        firstRow, firstCol = False, False
        for i in range(n):
            for j in range(m):
                if matrix[i][j] == 0:
                    if i == 0: 
                        firstRow = True
                    if j == 0:
                        firstCol = True
                    matrix[0][j] = 0
                    matrix[i][0] = 0
        
        for i in range(1, n):
            if matrix[i][0] == 0:
                for j in range(1, m):
                    matrix[i][j] = 0
        
        for j in range(1, m):
            if matrix[0][j] == 0:
                for i in range(1, n):
                    matrix[i][j] = 0
        if matrix[0][0] == 0:
            for i in range(max(n, m)):
                if i < n and firstCol:
                    matrix[i][0] = 0
                if i < m and firstRow:
                    matrix[0][i] = 0
```

