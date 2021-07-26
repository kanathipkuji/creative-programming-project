# Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/

## Solution: C++ STL function
### Language: C++

Partial sum function is the function that computes the partial sum of the sub list but it can be modified to find partial product instead.

The following code computes forward partial product of the list and stores it in *result*. Next, it computes backward partial product and stores it in *nums*. Finally, it combines these products by multiplying one by one.

```c++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> result(1, 1);
        partial_sum(nums.begin(), nums.end() - 1, back_inserter(result), multiplies<int>());
        partial_sum(nums.rbegin(), nums.rend() - 1, nums.rbegin(), multiplies<int>());
        transform(result.begin(), result.end() - 1, nums.begin() + 1, result.begin(), multiplies<int>());
        return result;
    }
};
```

