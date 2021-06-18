# Valid Palindrome
https://leetcode.com/problems/valid-palindrome/

## Solution: Linear Traversal
### Language: C++
### Time Complexity: O(n)

The trick is to remove non-alphanumeric characters from the string first, using erase() and remove_if() built-in function.
Then, do a linear search checking if the character on the opposite end is the same character or not.
Return false, if it is not, otherwise return true.

```C++
class Solution {
public:
    bool isPalindrome(string s) {
        s.erase(remove_if(s.begin(), s.end(), [](const char c) {
            return !isalpha(c) && !isdigit(c);
        }), s.end());
        
        for(int i = (s.size() - 1) / 2; i >= 0; --i) {
            if(tolower(s[i]) != tolower(s[s.size() - i - 1]))
                return false;
        }
        return true;
    }
};
```

