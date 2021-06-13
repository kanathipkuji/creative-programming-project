# Shortest Path to Get All Keys
https://leetcode.com/problems/shortest-path-to-get-all-keys/

## Solution: State Space Search
### Language: C++
### Time Complexity: O(nmk) where k is 2^m where m is the number of unique keys

The solution is a breadth first search on a graph with additional state, i.e., collected keys. 
The added state is a bitmask storing whether key *i* is collected, if so, i-th bit is 1.
Coordinate (i, j) with *k* hashing value is visited exactly once. Thus, time complexity is reduced to O(nmk).

```c++
class Solution {
    bool vis[30][30][64];
    
    int getKey(char c) {
        return islower(c) ? c - 'a' : c - 'A';
    } 
    
public:
    int shortestPathAllKeys(vector<string>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        int xx, yy, count = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == '@') {
                   xx = i, yy = j; 
                } else if (islower(grid[i][j])) {
                    ++count;
                }
            }
        }
        
        if (count == 0) return 0;
        
        const int gx[] = {-1, 0, 1, 0};
        const int gy[] = {0, -1, 0, 1};
        int x, y, b, bb, sz;
        int ok = (1 << count) - 1;
        int dist = 0;
        
        queue<tuple<int, int, int>> q;
        q.emplace(xx, yy, 0);
        vis[xx][yy][0] = true;
        
        while (!q.empty()) {
            sz = q.size();
            while (sz--) {
                tie(x, y, b) = q.front();
                q.pop();

                for (int i = 0; i < 4; ++i) {
                    xx = x + gx[i];
                    yy = y + gy[i];
                    if (xx < 0 || xx >= n || yy < 0 || yy >= m || grid[xx][yy] == '#') continue;
                    if (isupper(grid[xx][yy]) && !(b & (1 << getKey(grid[xx][yy])))) continue;

                    bb = b;

                    if (islower(grid[xx][yy])) {
                        bb = b | (1 << getKey(grid[xx][yy]));
                    }

                    if (vis[xx][yy][bb]) continue;

                    vis[xx][yy][bb] = true;
                    if (bb == ok) {
                        return dist + 1;
                    }
                    q.emplace(xx, yy, bb);
                }
            }
            
            ++dist;
            
        }
        return -1;
    }
};
```
