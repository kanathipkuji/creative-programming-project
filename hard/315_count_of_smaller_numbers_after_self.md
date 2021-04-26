# Count of Smaller Numbers After Self
https://leetcode.com/problems/count-of-smaller-numbers-after-self/

## 1st Solution: Merge Sort
### Language: C++
### Time Complexity: O(nlogn)

* 	Merge Sort the list (values zipped with their indices)
* 	In the merge function, keep track of how many numbers right pointer *r* have visited. Store the number in *rightCount*
* 	*rightCount* will be the number of smaller elements lying on the latter half at the current iteration.
* 	Add *rightCount* to the index the current left pointer is pointing to. 

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
