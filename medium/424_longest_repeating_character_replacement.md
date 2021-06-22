# Longest Repeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement/

## Solution: Two-Pointers Technique
### Language: C++
### Time Complexity: O(n)

First, iterate through all characters that will be replaced to (A to Z).
Assuming the character is *c*, we will find the maximum length of substring containing only character *c* with a maximum of *k* replacement.
To solve this, we maintain a maximum range of substring [l..r] such that the substring does not violate the rule, i.e., non-*c* characters in the range must not exceed *k*.
The condition can be written as follows.

* *r*-*l*+1 - freq[*c*] <= *k*

where freq[*c*] is the occurences of character *c* in the substring.

If the condition is satisfied, we track the maximum length of the substring. That value is the answer to the problem.

```c++
class Solution {
    vector<int> freq;
public:
    int characterReplacement(string s, int k) {
        int n = s.size(), l, ret = 0;
        for (int c = 0; c < 26; ++c) {
            freq.assign(26, 0);
            l = 0;
            for (int r = 0; r < n; ++r) {
                ++freq[s[r] - 'A'];
                while (l < r && r - l + 1 > freq[c] + k) {
                    --freq[s[l] - 'A'];
                    ++l;
                }
                ret = max(ret, r - l + 1);

            }
        }
        return ret;
    }
};
```

