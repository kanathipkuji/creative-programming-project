# Largest Number
https://leetcode.com/problems/largest-number/

## Solution: Custom Sorting
### Language: Python 3
### Time Complexity: O(nlogn)

We can sort an array of integer by comparing 2 elements in the following manner. 

* Every left element concatenated with right element is numerically greater than right element concatenated with left element.

After the array is sorted, simply join all elements in the array to form a string.

```python3
class Solution(object):
    def largestNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: str
        """
        res = sorted(nums, key=cmp_to_key(lambda x, y: -1 if str(x) + str(y) > str(y) + str(x) else 1))
        if all([x == 0 for x in res]):
            return '0'
        return ''.join(map(str, res))
```

