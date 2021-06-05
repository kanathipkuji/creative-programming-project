# Largest Rectangle in Histogram
https://leetcode.com/problems/largest-rectangle-in-histogram/

## Solution: Monotonic Stack
### Language: C++
### Time Complexity: O(n)

We maintain a monotonic stack that keep a key of elements in ascending order of its value.
It holds true that for each pair of indices adjacent in the monotonic stack, there will be no indices between those at which the height is less than the height of the height that the right element of the pair.
For example, let an adjacent pair of indices in a monotonic stack be (a, b).
All values between heights[a + 1] and heights[b], inclusively, are greater than heights[a].
For this reason, we can find the maximum area that starts from heights[a + 1] and ends at the current index by simply multiply the length with the height of the top of the stack.


```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> s;
        int ret = 0;
        heights.push_back(0);
        int n = heights.size(), u, height, prev;
        for (int i = 0; i < n; ++i) {
            height = heights[i];
            while (!s.empty() && heights[s.top()] >= height) {
                u = s.top();
                s.pop();
                
                prev = s.empty() ? -1 : s.top();
                ret = max(ret, (i - prev - 1) * heights[u]);
            }
            s.push(i);
        }
        return ret;
    }
};
```
