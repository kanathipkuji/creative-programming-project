# Reverse Bits
https://leetcode.com/problems/reverse-bits/

## Solution: Simulation of mathematical addition
### Language: C++
### Time Complexity: O(1)

First, store the number represented in base 2, in a string reversely. Then, calculate the base-10 integer represented by the string.   

```C++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        string s="";
        int i = 32;
        while(i--) {
            s += n % 2+ '0';
            n >>= 1;
        }
        int ret = 0;
        for(auto c: s) {
            ret <<= 1;
            ret += c - '0';
        }
        
        return ret;
    }
};
```

