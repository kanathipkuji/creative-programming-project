# Word Break
https://leetcode.com/problems/word-break/

## Solution: Dynamic Programming
### Language: Python 3

The dynamic state can be defined as follows.
 
dp[i] stores the boolean if words in dictionary can be combined to make substring s[0..i]. 

```python3
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        dp = [False]*(len(s) + 1)
        dp[0] = True
        S = set(wordDict)
        
        for i in range(len(s)):
            for j in range(i + 1):
                if not dp[j]: continue
                    
                if s[j:i+1] in S:
                    dp[i+1] = True
                    break
        return dp[-1]
```

