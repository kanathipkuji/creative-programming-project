# Kth Largest Element in an Array
https://leetcode.com/problems/kth-largest-element-in-an-array/

## Solution: Quick Select
### Language: C++
### Time Complexity: O(n) on average, O(n^2) in the worst case

*   Implement quick sort.
*   On each recursion of quick sort, if the pivot chosen is in the *k*-th position after partitioned, then it is the answer.
*   Because after partitioned, pivot will be moved to the right place if the array is all sorted. 

```c++
typedef vector<int> vi;

class Solution {
    vi::iterator first;
    int size;
    
    vi::iterator partition(vi::iterator l, vi::iterator r) {
        auto pivot = l;
        auto a = pivot + 1;
        for (auto it = a; it != r; ++it) {
            if (*it < *pivot) {
                iter_swap(it, a);
                ++a;
            }
        }
        --a;
        iter_swap(pivot, a);
        return a;
    }
    
    int quickSelect(vi::iterator l, vi::iterator r, int k) {
        if (l + 1 > r) return INT_MIN;
        auto pivot = partition(l, r);
        if (pivot - first == size - k) {
            return *pivot;
        }
        return max(quickSelect(l, pivot, k), quickSelect(pivot + 1, r, k)); 
    }
    
public:
    int findKthLargest(vector<int>& nums, int k) {
        first = nums.begin();
        size = nums.size();
        return quickSelect(nums.begin(), nums.end(), k);
    }
};
```

