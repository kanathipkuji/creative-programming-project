# Container With Most Water
https://leetcode.com/problems/container-with-most-water/

## Solution: Straightforward Implementation
### Language: C++

Iterate through the entre string *n* times, and generate the next string in each iteration.

```c++
class Solution {
public:
    string countAndSay(int n) {
        string s = "1";
        string next;
        --n;
        while (n--) {
            char prev = s[0];
            int count = 0;
            next = "";
            for (auto c: s) {
                if (c != prev) {
                    next += to_string(count);
                    next += prev;
                    prev = c;
                    count = 1;
                } else {
                    ++count;
                }
            }
            next += to_string(count);
            next += prev;
            s = next;
        }
        return s;
    }
};
```

