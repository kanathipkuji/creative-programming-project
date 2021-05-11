# Longest Increasing Path in a Matrix
https://leetcode.com/problems/longest-increasing-path-in-a-matrix/


## Solution: Topological sort & BFS
### Language: Python3
### Time Complexity: O(nm)

Smaller values should be traversed before larger values.
Thus, we can topologically sort each node (cell) with respect to its value.
Then, the longest increasing path is the number of levels of the Breadth First Search process.

Note: Topological sort is done by enqueueing nodes with least indegrees. 

```python
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        ds = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        n = len(matrix)
        m = len(matrix[0])
        indegree = [[0 for _ in range(m)] for _ in range(n)]
        for i in range(n):
            for j in range(m):
                for d in ds:
                    ii, jj = i + d[0], j + d[1]
                    if 0 <= ii < n and 0 <= jj < m and matrix[ii][jj] > matrix[i][j]:
                        indegree[ii][jj] += 1
    
        q = deque()
        for i in range(n):
            for j in range(m):
                if indegree[i][j] == 0:
                    q.append([i, j])
        
        count = 0
        while len(q) > 0:
            size = len(q)
            for i in range(size):
                cur = q.popleft()
                i, j = cur[0], cur[1]
                for d in ds:
                    ii, jj = i + d[0], j + d[1]
                    if 0 <= ii < n and 0 <= jj < m and matrix[ii][jj] > matrix[i][j] and indegree[ii][jj] > 0:
                        indegree[ii][jj] -= 1
                        if indegree[ii][jj] == 0:
                            q.append([ii, jj])
            count += 1
        return count
```
