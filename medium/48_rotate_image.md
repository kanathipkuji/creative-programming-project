# Rotate Image
https://leetcode.com/problems/rotate-image/

## Solution: 4-element swapping
### Language: C++
### Auxiliary Space Complexity: O(1)

First, observe that when the matrix is rotated, groups of four elements will be rotated. Each group consists of element from the following indices.
1. [i][j]
2. [n - j - 1][i]
3. [n - i - 1][n - j - 1]
4. [j][n - i - 1]

Thus, if we iterate from i and j to the quarter of the matrix size, we can swap those elements using constant space.

```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int tmp;
        int x = n / 2 + n % 2;
        int y = n / 2;
        for (int i = 0; i < x; ++i) {
            for (int j = 0; j < y; ++j) {
                tmp = matrix[n - j - 1][i];
                matrix[n - j - 1][i] = matrix[n - i - 1][n - j - 1];
                matrix[n - i - 1][n - j - 1] = matrix[j][n - i - 1];
                matrix[j][n - i - 1] = matrix[i][j];
                matrix[i][j] = tmp;
            }
        }
    }
};
```

