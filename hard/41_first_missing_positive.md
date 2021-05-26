# First Missing Positive
https://leetcode.com/problems/first-missing-positive/

## Solution: Indexing Trick
### Language: Python3
### Time Complexity: O(n)
### Space Complexity: O(1)

For each value *num* in the array, we mark the value belong to index *num* to indicate that the value *num* is found in the array.
For example, if *num* = 2 then the value at index 2 - 1 = 1 is marked.
After the pre-process is done, loop through the array from the beginning to see which index is the first one that is not marked.
The index will be the answer, i.e., the first positive integer that is missing.

```python3
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n = len(nums)
        for i, num in enumerate(nums):
            if num <= 0 or num > n:
                nums[i] = n + 1
        
        for num in nums:
            abNum = abs(num)
            abNum -= 1
            if 0 <= abNum < n and nums[abNum] > 0:
                nums[abNum] = -nums[abNum]
        
        for i, num in enumerate(nums):
            if num > 0:
                return i + 1
            
        return n + 1
```
