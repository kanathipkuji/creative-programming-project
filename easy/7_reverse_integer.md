#  Reverse Integer
https://leetcode.com/problems/reverse-integer/

## Solution: Linear Traversal
### Language: C++

This code uses string as a medium before converting it to integer.
However, it is necessary to check if is out of bound by checking whether the value before negating is less equal to the minimum value of integer.

```c++
class Solution {
public:
    int reverse(int x) {
        if (!x) return 0;
        int rev = 0;
        string s = "";
        bool neg = false;
    
        if (x < 0) {
            s += '-';
            
            if (x == INT_MIN) 
                return 0;
            x *= -1;
            neg = true;
        }
        int xx = abs(x);
        while (x) {
            s += x % 10 + '0';
            x /= 10;
        }
        cout << 'A';
        try {
            stoi(s);
        } catch (...) {
            return 0;
        }
        cout << 'B';
        return stoll(s);
    }
};
```

