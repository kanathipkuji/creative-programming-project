# Pow(x, n)
https://leetcode.com/problems/powx-n/

## Solution: log(n)-Power
### Language: C++

To find the value of x to the power of n, where n is a greater than a million, simple loop will result in time limit exceeded. Therefore, we use a different method to find the power.
The method is to square the base multiplier and multiply the multiplier to the result value wisely. In particular, it is multiplied when a 1-bit in *n* and a 1-bit in (1 << i) where i is the current loop number, matches.

```c++
class Solution {
    double positivePow(double x, long long n) {
        double ret = 1, mult = x;
        for (long long i = 1; i <= n ; i <<= 1) {
            if (i & n) {
                ret *= mult;
            }
            mult *= mult;
        }
        return ret;
    }
    
public:
    double myPow(double x, int n) {
        if (x == 1) return 1;
        if (x == 0) return 0;
        if (n > 0) {
            return positivePow(x, n);    
        } 
        if (n == 0) {
            return 1;
        } 
        return 1.0 / positivePow(x, -(long long)n);
    }
};
```

