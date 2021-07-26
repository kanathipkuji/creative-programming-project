# Search in Rotated Sorted Array
https://leetcode.com/problems/search-in-rotated-sorted-array/

## Solution: Utilizing Partition Point from C++ STL
### Language: C++
### Time Complexity: O(nlogn)

The solution is to find the first node whose value is greater than the first node of the array. This can be achieved by performing binary search. But the code below, utilize the function partition_point() which will binary search and find the point at which the value return from the given predicate function is false.

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if(nums.empty()) 
            return -1;
        auto f = begin(nums);
        auto l = end(nums);
        auto isDecreasing = [x = *f](int e) {
            return e >= x;
        };
        auto p = partition_point(f, l, isDecreasing);
        cout << p - f;
        auto it = lower_bound(f, p, target);
        if(it != p && *it == target)
            return it - f;
        it = lower_bound(p, l, target);
        if(it != l && *it == target)
            return it - f;
        return -1;
    }
};
```
