# Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/

## 1st Solution: Sorting
### Language: C++
### Time Complexity: O(nlogn)

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        if(nums.size() == 1)
            return nums[0];
        sort(nums.begin(), nums.end());
        int cur = INT_MAX, count = 0;
        for(auto& x: nums) {
            if(x == cur) {
                ++count;
                if(count > nums.size() / 2)
                    return x;
                continue;
            }
            count = 1;
            cur = x;
        }
        return 0;
    }
};
```

## 2nd Solution: Boyer-Moore Voting Algorithm
### Language: Python 3
### Time Complexity: O(n)

The algorithm adds up *count* when the same number is encountered, and subtracts from it when it encounters different number.

```python3
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = 0
        candidate = None
        for num in nums:
            if count == 0:
                candidate = num
            if num == candidate:
                count += 1
            else:
                count -= 1
                
        return candidate
```

