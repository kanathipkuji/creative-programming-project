# Longest Substring with At Least K Repeating Characters
https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/

## Solution 1st: Sliding Window Technique 
### Language: Python3
### Time Complexity: O(n)

*   Simplify the problem by dividing it into sub-problems
*   What is the answer if the satisfying longest substring contains exactly *maxNumUnique* unique characters?
*   For each sub-problem, apply sliding window technique to maintain a window that contains less than *maxNumUnique* unique characters.
*   While moving the two pointers (l, r), keep track of the number of unique characters and characters that appeared >= k times for all elements on the current window.

```
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        ans = 0
        for maxNumUnique in range(1, 27):
            l = 0
            freq = [0] * 26
            numUnique = numNoLessThanK = 0
            for r in range(len(s)):
                idx = ord(s[r]) - ord('a')
                if freq[idx] == 0:
                    numUnique += 1
                if freq[idx] == k - 1:
                    numNoLessThanK += 1
                freq[idx] += 1
                
                while numUnique > maxNumUnique:
                    idx = ord(s[l]) - ord('a')
                    freq[idx] -= 1
                    if freq[idx] == 0:
                        numUnique -= 1
                    if freq[idx] == k - 1:
                        numNoLessThanK -= 1
                    l += 1
                if numNoLessThanK == maxNumUnique:
                    ans = max(ans, r - l + 1)
        return ans
```

## Solution: Splitting into substrings
### Language: Python3
### Time Complexity: O(n)

*   Recursively split the string at the character appearing less than *k* times,
*   while storing the maximum length of substrings that satisfy the condition.

```
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        ss = set(s)
        for c in ss:
            if s.count(c) < k:
                return max(self.longestSubstring(subString, k) for subString in s.split(c))
        return len(s)
```
