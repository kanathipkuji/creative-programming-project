# Maximum Subarray
https://leetcode.com/problems/maximum-subarray/

## 1st Solution: Divide and Conquer
### Language: C++
### Time Complexity: O(nlogn)

One can take a divide and conquer approach to solve its sub-problems and combined those results and create a solution for bigger problems.
Given a subarray [l..r], one can find maximum sum subarray by either take maximum sum of [l..mid] or that of [mid + 1..r], or find the maximum that crosses index *mid*, e.g. any range [..mid..].

```c++
class Solution {
public:
    int findMaxCross(const vector<int>::iterator& l, const vector<int>::iterator& mid, const vector<int>::iterator& r) {
        int mxl, mxr;
        mxl = mxr = INT_MIN;
        int sum  = 0;
        for(auto it = mid; ; --it) {
            sum += *it;
            mxl = max(mxl, sum);
            if(it == l)
                break;
        }
        sum = 0;
        for(auto it = next(mid); ; ++it) {
            sum += *it;
            mxr = max(mxr, sum);
            if(it == r)
              break;
        }
        return max(max(mxl, mxr), mxl + mxr);
    }

    int findMaxSumInRange(const vector<int>::iterator& l, const vector<int>::iterator& r) {
        if(l == r)
            return *l;
        auto mid = l + (r - l) / 2;
        int mx = max(INT_MIN, findMaxSumInRange(l, mid));
        mx = max(mx, findMaxSumInRange(next(mid), r));
        mx = max(mx, findMaxCross(l, mid, r));
        return mx;
    }
    
    int maxSubArray(vector<int>& nums) {
        return findMaxSumInRange(begin(nums), end(nums) - 1);
    }
};
```

## 2nd Solution: Kadane's Algorithm
### Language: Python3
### Time Complexity: O(n)

We adopt Kadane's algorithm to find the maximum subarray. It is a dynamic programming approach that maintains a current sum and an overall maximum sum.

```python3
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        sum = 0
        maxSum = max(nums)
        if maxSum < 0: return maxSum
        for num in nums:
            sum = max(0, sum + num)
            maxSum = max(maxSum, sum)
        return maxSum
```


