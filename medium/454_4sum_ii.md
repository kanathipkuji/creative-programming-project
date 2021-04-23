# 4Sum II
https://leetcode.com/problems/4sum-ii/

## 1st Solution: Enumerating & Mapping
### Language: Python3
### Time Complexity: O(n^2)

*   Store a frequency of the value of nums1[i] + nums2[j] in a hashmap
*   For each nums3[m] + nums4[n] == - (nums1[i] + nums2[j]), add the frequency from the hashmap to the result. 

```
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        hashmap = defaultdict(int)
        for num1 in nums1:
            for num2 in nums2:
                hashmap[num1 + num2] += 1
        ans = 0
        for num3 in nums3:
            for num4 in nums4:
                ans += hashmap[- num3 - num4]
        return ans
```

Combining Python's list comprehension with collections.Counter() to count occurrences of elements
ans sum() function, the code above can be re-written as: 

```
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        hashmap = collections.Counter(num1 + num2 for num1 in nums1 for num2 in nums2)
        return sum(hashmap[- num3 - num4] for num3 in nums3 for num4 in nums4)
```

