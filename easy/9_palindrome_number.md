# Palindrome Number
https://leetcode.com/problems/palindrome-number/

## Solution: Simple Iteration on String
### Language: Python 3
### Time Complexity: O(n)

First, convert the integer into a string, then we perform a single iteration to check if characters on the opposite end is the same character or not.

```python3
class Solution:
    def isPalindrome(self, x: int) -> bool:
        s = str(x)
        if s[0] == '-':
            return False
        n = len(s)
        for i in range(n // 2):
            if s[i] != s[n - i - 1]:
                return False
        
        return True
            
```
