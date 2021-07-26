# Course Schedule II
https://leetcode.com/problems/course-schedule-ii/

## Solution: Topological Sort
### Language: C++

The solution is to topologically sort the list so that all prerequisite courses come first.

```c++
class Solution {
    vector<vector<int>> adj;
    vector<int> vis;
    vector<int> ans;
    
    bool dfs(int u) {
        vis[u] = 1;
        for(auto& v: adj[u]) {
            if(!vis[v]) {  
                if(!dfs(v)) return false;
            } else if(vis[v] == 1) {
                return false;
            }
        }
        ans.push_back(u);
        vis[u] = 2;
        return true;
    }
    
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        adj.assign(numCourses, vector<int>());
        for(auto &x: prerequisites) {
            adj[x[1]].push_back(x[0]);
        }
        vis.assign(numCourses, 0);
        for(int i = 0; i < numCourses; ++i)
            if(!vis[i])
                if(!dfs(i))
                    return vector<int>();
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

