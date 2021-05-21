# Next Permutation
https://leetcode.com/problems/next-permutation/

## Solution: 
### Language: C++
### Time Complexity: O(n)
### Space Complexity: O(1)


Any arrays of length *n* either contains a subarray [r..n-1] which is sorted in descending order, or otherwise, the array is already sorted in a descending order.

* In the first case, we can find the next permutation of the array by swapping element *r-1* with the first element from the right that is larger than element *r-1*.
* Then, simply reverse the subarray [r..n-1] to sort it in an ascending order.
* In the second case where the array is already sorted, then there is no next permutation, therefore we reverse the array.


```c++
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int l, r;
        l = r = nums.size() - 1;
        --l;
        while (l >= 0 && nums[l] >= nums[r]) {
            --l, --r;
        }
        if (l < 0) {
            reverse(nums.begin(), nums.end());
            return;
        }
        int k;
        for (k = nums.size() - 1; k > l && nums[k] <= nums[l]; --k) {}
        swap(nums[k], nums[l]);
        reverse(nums.begin() + r, nums.end());
    }
};
```

