# Longest Consecutive Sequence
https://leetcode.com/problems/longest-consecutive-sequence/


## 1st Solution: Transform and Conquer
### Language: Python3
### Time Complexity: O(nlogn)

* 	Pre-sort nums
* 	Iteratively increment current maximum length of consecutive subsequence
        achieved by comparing previous element with (current element - 1)
* 	Keep track of maximum length with another variable

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

## 2nd Solution: Utilizing Hashmap
### Language: Python3
### Time Complexity: O(n) on average

*       Store a set of nums
*       For each element *cur* with no consecutive element before it, i.e., *cur - 1* does not exist,
*       find the largest element belonging to the same consecutive sequence
*       Keep track of maximum difference between maximum and minimum element in the same sequence

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numsSet = set(nums)
        ans = 0
        for cur in numsSet:
            if cur - 1 not in numsSet:
                r = cur + 1
                while r in numsSet:
                    r += 1  
                ans = max(ans, r - cur)     
        return ans
```
