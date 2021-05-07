# Coin Change
https://leetcode.com/problems/coin-change/

## Solution: Dynamic Programming (0-1 Knapsack)
### Language: Pythons
### Time Complexity: O(amount * n) (n = number of coins)

One can defined the state of ks[][] as follows.
ks[i][j] is the minimum number of coins needed to sum up to exactly j, by using coins from denominations from coins[0..(i-1)].
But the latter dimension can be omitted because at any step j, there is no need to look further into step former than j - 1.

```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        ks = [amount + 1] * (amount + 1)
        ks[0] = 0
        for coin in coins:
            for i in range(coin, amount + 1):
                if ks[i - coin] <= amount:
                    ks[i] = min(ks[i], ks[i - coin] + 1)
        return ks[amount] if ks[amount] <= amount else -1
```

