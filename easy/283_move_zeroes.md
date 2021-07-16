# Move Zeroes
https://leetcode.com/problems/move-zeroes/

## Solution: Stable Partition
### Language: C++

I chose to use C++ built-in funciton: stable_partition() as it partitions the list from the condition and also maintains its relative position.

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        stable_partition(begin(nums), end(nums), [](int x){
            return x != 0;
        });
    }
};
```

