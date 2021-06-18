# Climbing Stairs
https://leetcode.com/problems/climbing-stairs/

## Solution: Compute n-th Fibonacci number
### Language: C++
### Time Complexity: O(n)

On the n-th step, the previous step can either be from (n - 2)-th step or (n - 1)-th step. As this resembles Fibonacci sequence, we can solve the problem by computing that Fibonacci number. 

```c++
class Solution {
public:
    int climbStairs(int n) {
        int a = 0, b = 1, c;
        while(n--) {
            c = a + b;
            a = b;
            b = c;
        }
        return c;
    }
};
```

