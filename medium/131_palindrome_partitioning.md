# Palindrome Partitioning
https://leetcode.com/problems/palindrome-partitioning/

## 1st Solution: Depth First Search
### Language: Python3
### Time Complexity: O(n*2^n) where *n* is the length of the string

The solution is to recursively divide string into substrings, and check if the substring is palindrome. If all the substrings are palindrome, and there are no character left, append the result to the answer list.

```python3
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        ret = []
        cur = []        
        
        def isPalindrome(s, l, r):
            while l < r:
                if s[l] != s[r]:
                    return False
                l += 1
                r -= 1
            return True
        
        def dfs(idx):            
            
            if idx == len(s):
                ret.append(cur[:])
                return
        
            for i in range(idx, len(s)):
                if isPalindrome(s, idx, i):
                    cur.append(s[idx:i+1])
                    dfs(i + 1)
                    cur.pop()
        dfs(0)    
        
        return ret
```

## 2nd Solution: Depth First Search with Dynamic Programming
### Language: Python3
### Time Complexity: O(n*2^n) where *n* is the length of the string

In this approach, instead of using loops to check palindromes, it uses an array that keep if substring in range [a..b] is a palindrome or not.

```python3
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        ret = []
        cur = []        
        n = len(s)
        isPal = [[0] * n for _ in range(n)]
        
        def dfs(idx):            
            
            if idx == n:
                ret.append(cur[:])
                return
        
            for i in range(idx, n):
                if s[idx] == s[i] and (i - idx <= 2 or isPal[idx + 1][i - 1]):
                    isPal[idx][i] = True
                    cur.append(s[idx:i+1])
                    dfs(i + 1)
                    cur.pop()
        dfs(0)    
        
        return ret
```

