# Happy Number
https://leetcode.com/problems/happy-number/

## Solution: Searching with memoization
### Language: C++

Simulate the process until we encounter the number already calculated (meaning it enters an infinite loop in which case return false), or the number is 1 in which case return true.

```C++
class Solution {
public:
    bool arr[10005]{};
    int sumOfSquare(int n) {
        int ret = 0, m;
        while(n > 0) {
            m = n%10;
            ret += m*m;
            n /= 10;
        }
        return ret;
    }
    
    bool isHappy(int n) {
        bool first = true;
        while(true) {
            if(!first) {
                if(arr[n]) 
                    return false;
                arr[n] = true;
                
            }
            first = false;
            n = sumOfSquare(n);
            if(n == 1)
                return true;
            
        }
        
    }
};
```

