# Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring/

## 1st Solution: Sliding Window
### Language: C++
### Time Complexity: O(|s| + |t|) where |s| is the length of string s, and |t| is the length of string t.

This approach applies sliding window technique to maintain a block of minimum size that contains all characters from string t.
This works because if a substring [l..r] contains all characters from t, then it is unnecessary to consider any characters before index l. In other words, we can track the minimum value at this point, and move l to the right by 1 unit. 

To maintain the property of the window, the solution keep a list of frequency of characters in the window, and check if it matches the frequency of characters in string t.

```c++
class Solution {
    int freq[52], cFreq[52];
    
    bool isValid(string &s) {
        for (int i = 0; i < 52; ++i) {
            if (freq[i] < cFreq[i]) return false;
        }
        return true;
    }
    
    int charToInt(char c) {
        if (isupper(c)) {
            return c - 'A';
        } else {
            return c - 'a' + 26;
        }
    }
    
public:
    string minWindow(string s, string t) {
        for (char c: t) {
            ++cFreq[charToInt(c)];
        }
        int l, r, ret;
        l = r = 0;
        ret = INT_MAX;
        int L = -1, R = -1;
        while (r < s.size()) {
            ++freq[charToInt(s[r])];
            while (l < r && isValid(s)) {
                --freq[charToInt(s[l])];
                if (ret > r - l + 1) {
                    ret = r - l + 1;
                    L = l, R = r;
                }
                ++l;

            }
            if (isValid(s)) {
                if (ret > r - l + 1) {
                    ret = r - l + 1;
                    L = l, R = r;
                }
            }
            ++r;
        }
        if (L == -1 && R == -1) return "";
        return s.substr(L, ret);
    }
};
```

## 2nd Solution: Optimized Sliding Window
### Language: C++
### Time Complexity: O(|s| + |t|) where |s| is the length of string s, and |t| is the length of string t.

Instead of looping for all distinct characters when checking validity, we create a variable to store the number of distinct characters that already fully matched with string t.
This way, checking validity decreases to O(1).


```c++
class Solution {
    int freq[52];
    
    int charToInt(char c) {
        if (isupper(c)) {
            return c - 'A';
        } else {
            return c - 'a' + 26;
        }
    }
    
public:
    string minWindow(string s, string t) {
        int count = 0, idx;
        for (char c: t) {
            idx = charToInt(c);
            if (freq[idx] == 0) ++count;
            ++freq[idx];
        }
        int l, r, ret;
        l = r = 0;
        ret = INT_MAX;
        int L = -1, R = -1;
        while (r < s.size()) {
            if (--freq[charToInt(s[r])] == 0) {
                --count;
            }
            
            while (l <= r && count == 0) {
                if (ret > r - l + 1) {
                    ret = r - l + 1;
                    L = l, R = r;
                }
                if (freq[charToInt(s[l])]++ == 0) {
                    ++count;
                }
                ++l;
            }
            ++r;
        }
        if (L == -1 && R == -1) return "";
        return s.substr(L, ret);
    }
};
```

