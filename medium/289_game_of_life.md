# Game Of Life
https://leetcode.com/problemset/top-interview-questions/

## Solution: Bitmask
### Language: Python3
### Time Complexity: O(nm)
### Space Complexity: O(1)

To avoid the use of auxiliary space, we can modify the value of the table so that it keeps information from both before and after updated.
The solution is to use the second bit to store the result, by compute the old value with |= 2.
Then, after the table is all processed, we shift the bit by 1 unit to the right in order to retrieve the updated value.

```
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        n = len(board)
        m = len(board[0])
        count = 0
        for i in range(n):
            for j in range(m):
                count = 0
                for dx in range(-1, 2):
                    for dy in range(-1, 2):
                        ii = i + dx
                        jj = j + dy
                        if 0 <= ii < n and 0 <= jj < m:
                            count += board[ii][jj] & 1
                if count == 3 or (board[i][j] and 3 <= count <= 4):
                    board[i][j] |= 2
        
        for i in range(n):
            for j in range(m):
                board[i][j] >>= 1
        
```

