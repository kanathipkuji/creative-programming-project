# Sum of Two Integers
https://leetcode.com/problems/sum-of-two-integers/

## Solution: Bit Manipulation
### Language: C++

The solution below add two integers using bit manipulation by adding bits that are different and carrying the bit appearing in both integers to the next addition of the carry integer and the result from the last addition.

```C++
class Solution {
public:
    int getSum(int a, int b) {
        int tmp;
        while (b != 0) {
            tmp = a ^ b;
            b = (unsigned)(a & b) << 1;
            a = tmp;
        }
        return a;
    }
};
```

