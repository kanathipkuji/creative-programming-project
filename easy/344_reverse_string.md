# Reverse String
https://leetcode.com/problems/reverse-string/

## Solution: Swapping
### Language: Python 3
### Time Complexity: O(n)

The code below swaps elements from opposite sides until it reaches the middle.

```python3
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        n = len(s)
        for i in range(n // 2):
            s[i], s[n - i - 1] = s[n - i - 1], s[i]
```

