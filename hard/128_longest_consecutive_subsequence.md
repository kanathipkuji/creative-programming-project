# Longest Consecutive Subsequence
https://leetcode.com/problems/longest-consecutive-sequence/


## 1st Solution: Transform and Conquer
### Language: Python3
### Time Complexity: O(nlogn)

* 		Pre-sort nums
* 		Iteratively increment current maximum length of consecutive subsequence
        achieved by comparing previous element with (current element - 1)
* 		Keep track of maximum length with another variable

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums.sort()
        prev = 10000000002
        count = ans = 0
        for num in nums:
            if prev == num: continue;
            if prev != num - 1:
                count = 1
            else:
                count += 1
            prev = num
            ans = max(ans, count)
        return ans;
```

