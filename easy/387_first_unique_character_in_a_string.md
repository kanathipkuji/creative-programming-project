# First Unique Character in a String
https://leetcode.com/problems/valid-palindrome/

## Solution: Hash Map
### Language: C++
### Time Complexity: O(n)
### Space Complexity: O(1)

We create an array of a fixed size to store values as a hash map, then we iterate through characters from the beginning and look whether its frequency is 1 or not.

```C++
class Solution {
    int hashMap[27];
public:
    int firstUniqChar(string s) {
        for(auto& c: s)
            ++hashMap[c - 'a'];
        int idx = 0;
        for(auto& c: s) {
            if(hashMap[c - 'a'] == 1)
                return idx;
            ++idx;
        }
        return -1;
                
    }
};
```

