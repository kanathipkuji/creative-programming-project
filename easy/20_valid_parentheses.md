# Valid Parentheses
https://leetcode.com/problems/valid-parentheses/

## Solution: Implementation using stack
### Language: C++
### Time Complexity: O(n)

We maintain a stack that store open parentheses and pop the top out if the corresponding parenthesis is found.

```python3
class Solution:
    def isValid(self, s: str) -> bool:
        parens = []
        pairs = {')': '(', ']': '[', '}': '{'}
        for c in s:
            if c == ')' or c == ']' or c == '}':
                if len(parens) == 0 or pairs[c] != parens[-1]:
                    return False
                parens.pop()
            else:
                parens.append(c)
        return len(parens) == 0

```

