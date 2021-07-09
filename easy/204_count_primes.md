# Count Primes
https://leetcode.com/problems/count-primes/

## Solution: Sieve of Eratosthenes
### Language: Python 3

The code below uses the sieve of Eratosthenes to screen out non-prime numbers. Note that we only need to screen those numbers until \sqrt(n).

```python3
class Solution:
    def countPrimes(self, n: int) -> int:
        notPrime = [False] * n
        ret = 0
        for i in range(2, n):
            if i * i >= n: break
            if notPrime[i]: continue
            for j in range(2 * i, n, i):
                notPrime[j] = True
        for i in range(2, n):
            if notPrime[i] == False:
                ret += 1
        return ret
```

