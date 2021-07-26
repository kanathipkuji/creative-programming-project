# Search a 2D Matrix II
https://leetcode.com/problems/search-a-2d-matrix-ii/

## Solution: Linear Search
### Language: Python 3
### Time Complexity: O(n)

One solution is to do a linear search starting from the top right corner.
If the target value is less than the current cell, we can ignore current column and every column to the right. The same strategy applies when the target value is greater than current node.

```python3
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        n = len(matrix)
        m = len(matrix[0])
        i, j = 0, m - 1
        while i < n and j >= 0:
            # print(i, j, matrix[i][j])
            if target < matrix[i][j]:
                j -= 1
            elif target > matrix[i][j]:
                i += 1
            else:
                return True
            
            
        return False 
```
