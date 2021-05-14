# Kth Largest Element in an Array
https://leetcode.com/problems/kth-largest-element-in-an-array/

## Solution: Sliding Window
### Language: Python3
### Time Complexity: O(n)

Maintain a sliding window with the following property.

* All elements in the window are unique.

Specifically, keep track of frequencies of each character in the window. The goal is to keep each frequency no more than 1.
Finally, track the maximum length of each sliding window. 

```python3
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        freq = defaultdict(int)
        l = ans = 0
        for r, c in enumerate(s):
            freq[c] += 1
            while freq[c] > 1:
                freq[s[l]] -= 1
                l += 1
            ans = max(ans, r - l + 1)
            
        return ans
```

