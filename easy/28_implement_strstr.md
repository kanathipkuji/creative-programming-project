# Implement strStr()
https://leetcode.com/problems/implement-strstr/

## Solution: Brute Force Implementation
### Language: Python
### Time Complexity: O(nm)

The following code is a brute force implementation that find a matching string one by one.

```python3
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle: return 0
        n = len(haystack)
        m = len(needle)
        for i in range(n - m + 1):
            count = 0
            for j in range(m):
                if haystack[i + j] != needle[j]:
                    break
                count += 1
            if count == m:
                return i
        return -1
```

