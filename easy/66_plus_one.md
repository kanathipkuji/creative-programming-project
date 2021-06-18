# Plus One
https://leetcode.com/problems/plus-one/

## Solution: Simulation of mathematical addition
### Language: C++
### Time Complexity: O(n)

We must do the work from the less significant digit, meaning increasing the last digit by 1, while storing the carry value if the sum exceeds 9.

```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        vector<int> ret;
        int plus = 1;
        for(int i = digits.size()-1; i >= 0; --i) {
            if(plus) {
                if(digits[i] == 9) {
                    digits[i] = 0;
                } else {
                    ++digits[i];
                    plus = 0;
                }
            }
            ret.push_back(digits[i]);
        }
        if(plus)
            ret.push_back(1);
        reverse(ret.begin(), ret.end());
        return ret;
    }
};
```

