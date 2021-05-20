# Generate Parentheses
https://leetcode.com/problems/generate-parentheses/

## Solution: Complete Search
### Language: Python3

The solution is to perform complete search by using recursive function with nonlocal variables storing current string pattern *cur*.
The character ')' will be added to *cur* as long as open parentheses exceeds close parentheses.

```python3
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        cur = []
        def gen(n, leftPar, rightPar):
            nonlocal res
            nonlocal cur
            if leftPar > n or rightPar > n:
                return
            if leftPar == n and rightPar == n:
                res.append(''.join(cur))
                return
            cur += '('
            gen(n, leftPar + 1, rightPar)
            cur.pop()
            if leftPar > rightPar:
                cur += ')'
                gen(n, leftPar, rightPar + 1)
                cur.pop()
            
        gen(n, 0, 0)
        return res
```

