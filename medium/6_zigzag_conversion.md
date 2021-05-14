# ZigZag Conversion
https://leetcode.com/problems/zigzag-conversion/solution/

## Solution: Access Index by Row
### Language: C++

The main observation is that we can access the index of the given array wisely, so that we can push the character visited to the result string one by one.

```c++
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1) {
            return s;
        }
        string ret = "";
        int n = s.length();
        int mod = 2 * (numRows - 1);
        int row = 0;
        int id = row, id2;
        while (row < numRows && id < n) {
            ret += s[id];
                    
            if (row > 0 && row < numRows - 1) {
                id2 = id + 2 * (numRows - row - 1);
                if (id2 < n)
                    ret += s[id2];
                else {
                    ++row;
                    id = row;
                    continue;
                }
            }
            id += mod;
            if (id >= n) {
                ++row;
                id = row;
            }
        }
        return ret;
    }
};
```
