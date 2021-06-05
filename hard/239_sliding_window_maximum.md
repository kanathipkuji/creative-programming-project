# Sliding Window Maximum
https://leetcode.com/problems/sliding-window-maximum/

## Solution: Sliding window with monotonic deque
### Language: C++
### Time Complexity: O(n)

Maintain a deque of elements in the window of size *k*, with properties as follows.

* Elements in the deque of the current window contains no elements outside the window.
* Elements are sorted such that the largest element is on the left.

This properties guarantee that the first element of the deque is the maximum element in the current window.

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> d;
        vector<int> ret;
        ret.reserve(nums.size() - k + 1);
        for (int i = 0; i < nums.size(); ++i) {
            while (!d.empty() and d.front() <= i - k) {
                d.pop_front();
            }
            while (!d.empty() and nums[d.back()] <= nums[i]) {
                d.pop_back();
            }
            d.push_back(i);
            
            if (i >= k - 1)
                ret.push_back(nums[d.front()]);
        }
        return ret;
    }
};
```
