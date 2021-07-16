# Valid Anagram
https://leetcode.com/problems/maximum-depth-of-binary-tree/

## Solution: Python Collections
### Language: Python 3

Counter() is a function returning a dictionary of characters as keys and their frequencies as values.
Two string are considered anagram if frequencies of all characters are the same.

```python3
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        count = Counter(s)
        count2 = Counter(t)
        return count == count2
```

