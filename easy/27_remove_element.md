# Length of Last Word
https://leetcode.com/problems/length-of-last-word/

## Solution: Spliting String into Substrings
### Language: Python 3

The function strip() is called to erase all leading and trailing white spaces, and the function split() is used to split() all words (substrings not containing spaces) into a list. Finally, we extract the last split substring from the list.

```python3
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        return len(s.strip().split(' ')[-1])
```
