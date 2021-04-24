# Longest Substring with At Least K Repeating Characters
https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/

## Solution: Sliding Window Technique 
### Language: Python3
### Time Complexity: O(n)

*   Simplify the problem by dividing it into sub-problems
What is the answer if the satisfying longest substring contains only *maxNumUnique*
*   For each nums3[m] + nums4[n] == - (nums1[i] + nums2[j]), add the frequency from the hashmap to the result. 

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
