# Excel Sheet Column Number
https://leetcode.com/problemset/all/?listId=wpwgkgt

## Solution: Converting base
### Language: C++

Excel sheet number is expressed in base 26, so we can change the base to 10 and print out the result.

```c++
class Solution {
public:
    int titleToNumber(string s) {
        int ret = 0;
        for(auto& c: s) {
            ret *= 26;
            ret += c - 'A' + 1;
        }
        return ret;
    }
};
```

