# Fizz Buzz
https://leetcode.com/problems/fizz-buzz/

## Solution: Straightforward Implementation
### Language: Python
### Time Complexity: O(n)

```python3
class Solution:
    def fizzBuzz(self, n: int) -> List[str]:
        ret = []
        for i in range(1, n + 1):
            if i % 3 == 0 or i % 5 == 0:
                cur = ""
                if i % 3 == 0:
                    cur += "Fizz"
                if i % 5 == 0:
                    cur += "Buzz"
                ret.append(cur)
            else:
                ret.append(str(i))
                
        return ret
```

