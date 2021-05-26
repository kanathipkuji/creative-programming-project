# Permutation Sequence
https://leetcode.com/problems/permutation-sequence/

## Solution: Utilizing Set (BBST) data structure
### Language: C++
### Time Complexity: O(nlogn)

Given *k*, it is possible to calculate the first value appearing in k-th permutation pf length *n* by dividing *k* by *n!*.
Now, notice that permutation of length *n* consist of *n* permutations of length *n-1*.
Therefore, we can use the same strategy but in this case the value would be different for each permutation of length *n-1*.
For example, given an array [1, 2, 3, 4, 5], the k-th permutation with 2 and 5 as the first index might be [2, 3, 1, 4, 5] and [5, 2, 1, 3, 4], respectively.
In this case, [3, 1, 4, 5] and [2, 1, 3, 4] belong to the same rank, i.e. the order regardless of values. However, they contain different values.
So, when calculating the value belonging to each index, it should be used in conjunction with C++ Set which can insert and delete unique values in O(logn) time complexity.

```c++
class Solution {
    vector<long long> fact;
    set<int> S;
    
    char getItem(int idx) {
        auto it = S.begin();
        advance(it, idx);
        char ret = *it + '0';
        S.erase(it);
        return ret;
    }
    
public:
    string getPermutation(int n, int k) {
        int i;
        auto it = S.begin();
        fact.push_back(1);
        for(i = 1; i <= n; ++i) {
            it = S.insert(it, i);
            fact.push_back(fact.back() * i);
        }
        string ret = "";
        --k;
        for(i = n - 1; i; --i) {
            ret += getItem(k / fact[i]);
            k %= fact[i];
        }
        ret += *S.begin() + '0';
        return ret;
    }
};
```
