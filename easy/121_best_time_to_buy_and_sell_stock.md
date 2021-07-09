# Best Time to Buy and Sell Stock
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

## Solution: Tracking min and max
### Language: Python 3
### Time Complexity: O(n)

We track a minimum price on each iteration while keeping track of the maximum difference between minimum price and current price. 

```python3
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        ret = 0
        mn = float('inf')
        for price in prices:
            mn = min(mn, price)
            ret = max(ret, price - mn)
        return ret
```

