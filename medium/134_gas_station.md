# Gas Station
https://leetcode.com/problems/surrounded-regions/

## Solution: Sum of Difference
### Language: Python 3

The solution tries to add up the difference betweem gas and cost on each index. Whenever the sum is negative, that means up until the index there are no stations that we can start at, in which case we reset the sum and stores index of the next station as an answer. 

```python3
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        n = len(gas)
        sum = 0
        ret = 0
        for i in range(2*n):
            sum += gas[i % n] - cost[i % n]
            if sum < 0:
                sum = 0
                ret = i + 1
        return -1 if ret > n else ret
```

