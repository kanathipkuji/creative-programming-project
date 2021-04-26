# Count of Smaller Numbers After Self
https://leetcode.com/problems/count-of-smaller-numbers-after-self/

## 1st Solution: Merge Sort
### Language: C++
### Time Complexity: O(nlogn)

* 	Merge Sort the list (values zipped with their indices)
* 	In the merge function, keep track of how many numbers right pointer *r* have visited. Store the number in *rightCount*
* 	*rightCount* will be the number of smaller elements lying on the latter half at the current iteration.
* 	Add *rightCount* to the index the current left pointer is pointing to. 

```
typedef vector<pair<int, int>> vii;

class Solution {
    vector<int> ans;
    
    void merge(vii::iterator l, vii::iterator mid, vii::iterator r) {
        auto l1 = l, l2 = mid;
        int count = 0, idx = 0, rightCount = 0;
        vii tmp(r - l);
        while (l1 < mid && l2 < r) {
            if (l1->first <= l2->first) {
                tmp[idx++] = *l1;
                ans[l1->second] += rightCount;
                ++l1;
            } else {
                tmp[idx++] = *l2;
                ++rightCount;
                ++l2;
            }
        }
        while (l1 < mid) {
            tmp[idx++] = *l1;
            ans[l1->second] += rightCount;
            ++l1;
        }
        while (l2 < r) {
            tmp[idx++] = *l2;
            ++l2;
        }
        auto it = l;
        idx = 0;
        while (it != r) {
            *it = tmp[idx++];
            ++it;
        }
    }
    
    void mergeSort(vii::iterator l, vii::iterator r) {
        if (l + 1 == r) return;
        auto mid = (r - l) / 2  + l;
        mergeSort(l, mid);         
        mergeSort(mid, r);
        merge(l, mid, r);
    }
public:
    vector<int> countSmaller(vector<int>& nums) {
        int i = 0;
        vii v;
        ans.resize(nums.size());
        for (auto num: nums) {
            v.emplace_back(num, i);
            ++i;
        }
        mergeSort(v.begin(), v.end());
        return ans;
    }
};
```
