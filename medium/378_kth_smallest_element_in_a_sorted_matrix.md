# Kth Smallest Element in a Sorted Matrix
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/

## 1st Solution: Naive Solution
### Language: Python3
### Time Complexity: O(n^2\*logn)

*   Flatten a matrix to a sorted list

```python3
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        l = sorted([cell for row in matrix for cell in row])
        return l[k - 1]
```


## 2nd Solution: Binary Search
### Language: Python3
### Time Complexity: O(log(maxVal) * n)

*   Binary Search on a value in range -10^9 to 10^9
*   For each middle value *mid*, find the number of elements that are less than or equal to *mid*, let *count* store the result.
*   This can be implemented in O(n) by iterating from the top-right corner.
*   If *count* is less than k, this means *mid* is less than the *k*th smallest element, thus left-half of the range should be discarded.

```python3
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        l = -1e9
        r = 1e9
        ans = 0
        
        while l < r:
            mid = l + (r - l) // 2
            count = 0
            col = len(matrix[0]) - 1
            for row in range(len(matrix)):
                while col >= 0 and matrix[row][col] > mid:
                    col -= 1
                count += col + 1
            
            if count < k:
                l = mid + 1
            else:
                r = mid
        
        return int(l)
```

