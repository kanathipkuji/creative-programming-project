# Kth Smallest Element in a Sorted Matrix
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/

## 1st Solution: Naive Solution
### Language: Python3
### Time Complexity: O(n^2\*logn)

*   Flatten a matrix to a sorted list

```
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        l = sorted([cell for row in matrix for cell in row])
        return l[k - 1]
```


## 2nd Solution: Dynamic Programming
### Language: Python3
### Time Complexity: O(nlogn)

*   Create an array which is always sorted in ascending order with the following properties.
*   Element at index *i* stores a tail (last element) of IS with length *i* + 1.
*   Thus, the length of LIS is equal to the length of IS at index *n* - 1 of the previously defined array.

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        v = []
        for num in nums:
            idx = bisect_left(v, num)
            if idx == len(v):
                v.append(num)
            else:
                v[idx] = num
        return len(v)
```

