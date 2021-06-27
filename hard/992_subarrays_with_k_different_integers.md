# Subarrays with K Different Integers
https://leetcode.com/problems/longest-duplicate-substring/

## Solution: Two-Pointers Technique
### Language: C++
### Time Complexity: O(n)

The idea is to maintain a range in which there are no more than *k* unique integers.
We also keep track of prefixes of the range that does not contribute to all characters being unique.
The number of subarray ending at index *r* that satisfies the condition is the number of prefixes plus 1, when the maintained range contains *k* unique characters.

```c++
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        int l = 0;
        int n = nums.size();
        vector<int> freq(n);
        int cur, countUnique = 0, countPrefix = 0;
        int ret = 0;
        for (int r = 0; r < n; ++r) {
            cur = --nums[r];
            if (freq[cur]++ == 0) {
                ++countUnique;                
            }
            
            while (countUnique > k) {
                --countUnique;
                --freq[nums[l]];
                ++l;
                countPrefix = 0;
            }
            while (freq[nums[l]] > 1) {
                ++countPrefix;
                --freq[nums[l]];
                ++l;
            }
            if (countUnique == k)
                ret += countPrefix + 1;
        }
        return ret;
    }
};
```
