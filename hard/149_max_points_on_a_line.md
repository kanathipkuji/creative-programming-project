# Max Points on a Line
https://leetcode.com/problems/max-points-on-a-line/

## Solution: Hashing slope 
### Language: C++
### Time Complexity: O(n^2logn)

The idea is to divide the problem into n sub-problems asking for maximum points in a line passing point *i*.
For each sub-problem, create a hash map to store the number of lines with a specific slope. 
In this case, we avoid storing a double value of the slope as a key as it might incur some floating-point precision error.
Instead, we store a pair of difference in x and y values as a key.

```c++
class Solution {
    int maxPointsContainingPointI(vector<vector<int>>& points, int i) {
        map<pair<int, int>, int> umap;
        int n = points.size(), gcd, dx, dy;
        int ret = 1;
        for (int j = 0; j < n; ++j) {
            if (j == i) continue;
            dx = points[i][0] - points[j][0];
            dy = points[i][1] - points[j][1];
            gcd = __gcd(dy, dx);
            
            auto it = umap.find({dy / gcd, dx / gcd});
            if (it == umap.end()) {
                umap[{dy /gcd, dx / gcd}] = 1;
            } else {
                ++(it->second);
                ret = max(ret, it->second);
            }
        }
        return ret + 1;
    }
    
public:
    int maxPoints(vector<vector<int>>& points) {
        if (points.size() <= 2) {
            return points.size();
        }
        int n = points.size();
        int ans = 1;
        for (int i = 0; i < n; ++i) {
            ans = max(ans, maxPointsContainingPointI(points, i));
        }
        return ans;
    }
};
```
