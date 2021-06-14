# Permutations
https://leetcode.com/problems/permutations/

## Solution: Johnson and Trotter's Algorithm
### Language: C++

The algorithm provides an approach to find next permutation in a sorted order of all permutations, in linear time to the size of an array.
In C++, the algorithm is captured in function *next_permutation()*. Thus, sorting the array, then calling the function should solve the problem easily.

```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ret;
        sort(nums.begin(), nums.end());
        do {
            ret.push_back(nums);
        } while (next_permutation(nums.begin(), nums.end()));
        return ret;
    }
};
```

