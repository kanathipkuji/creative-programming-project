# Unique Path III
https://leetcode.com/problems/unique-paths-iii/

## 1st Solution: Brute Force
### Language: Python3

The problem can be solved using brute force by keeping the number of unique cells not visiting so far. If we reach the final cell with the number equal to 0, 
then the path has visited all cells in the table. 

```python3
class Solution:
    def uniquePathsIII(self, grid: List[List[int]]) -> int:
        ret = 0
        n = len(grid)
        m = len(grid[0])
        empty = 1
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    x, y = i, j
                elif grid[i][j] == 0:
                    empty += 1
        
        def dfs(x, y, empty):
            nonlocal ret
            if not (0 <= x < n and 0 <= y < m and grid[x][y] >= 0): return
            if grid[x][y] == 2:
                ret += empty == 0
                return
            grid[x][y] = -1
            dfs(x + 1, y, empty - 1)
            dfs(x - 1, y, empty - 1)
            dfs(x, y + 1, empty - 1)
            dfs(x, y - 1, empty - 1)
            grid[x][y] = 0
            
            
        dfs(x, y, empty)
        return ret
```
